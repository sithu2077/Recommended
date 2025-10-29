**Void Linux setup portable and reproducible**, including both packages _and_ configs.

---

## 🧩 What you want to preserve

When you say “configuration,” that can include several layers:

|Type|Examples|Where it lives|
|---|---|---|
|User configs|`.bashrc`, `.vimrc`, `.config/*`|In your home dir|
|System configs|`/etc/*`|System-wide settings|
|Services|runit service definitions|`/etc/sv`, `/var/service`|
|Environment|Shell env vars, locales, hostname, etc.|`/etc/profile`, `/etc/hostname`|
|Users / groups|`/etc/passwd`, `/etc/group`, `/etc/shadow`|System files|

---

## 🧰 1. Export installed packages

(From previous step)

```bash
xbps-query -l | awk '/ii/ {print $2}' > pkglist.txt
```

---

## 🧰 2. Backup configuration files

You can use `rsync` to back up only config directories:

```bash
sudo rsync -av --progress /etc/ etc_backup/
```

Or more selectively:

```bash
sudo rsync -av /etc/{xbps,sv,hostname,rc.conf,network,profile.d} etc_backup/
```

This preserves:

- Package sources
    
- Service definitions
    
- Network and environment configs
    

---

## 🧰 3. Backup user configuration (dotfiles)

For your user-level configs:

```bash
rsync -av --progress ~/.config/ ~/dotfiles/.config/
rsync -av ~/.bashrc ~/.vimrc ~/dotfiles/
```

You can then **version control** that directory with Git:

```bash
cd ~/dotfiles
git init
git add .
git commit -m "My Void Linux setup"
```

Later, clone it on a new machine and symlink it:

```bash
ln -sf ~/dotfiles/.config ~/.config
ln -sf ~/dotfiles/.bashrc ~/.bashrc
```

Or use a tool like **GNU Stow**:

```bash
sudo xbps-install -S stow
stow bash vim config
```

---

## 🧰 4. Copy runit services

Void Linux uses **runit**, so to replicate service configuration:

```bash
sudo rsync -av /etc/sv/ sv_backup/
sudo rsync -av /var/service/ var_service_backup/
```

Then, on the new machine:

```bash
sudo rsync -av sv_backup/ /etc/sv/
sudo rsync -av var_service_backup/ /var/service/
```

---

## 🧰 5. Restore on the new machine

After setting up Void on the target system:

```bash
# Install packages
sudo xbps-install -S $(cat pkglist.txt)

# Restore system configs
sudo rsync -av etc_backup/ /etc/

# Restore user configs
rsync -av ~/dotfiles/ ~/
```

Restart services or reboot if needed.

---

## 🧰 6. Optional: Automate all this

You can wrap this into one Bash script (`void-backup.sh`):

```bash
#!/bin/bash
set -e

BACKUP_DIR="$HOME/void-backup-$(date +%F)"
mkdir -p "$BACKUP_DIR"

echo "[+] Exporting package list..."
xbps-query -l | awk '/ii/ {print $2}' > "$BACKUP_DIR/pkglist.txt"

echo "[+] Backing up /etc configuration..."
sudo rsync -a --exclude='/etc/ssl' /etc "$BACKUP_DIR/"

echo "[+] Backing up user config..."
rsync -a ~/.config "$BACKUP_DIR/"
cp ~/.bashrc ~/.zshrc "$BACKUP_DIR/" 2>/dev/null || true

echo "Backup complete at $BACKUP_DIR"
```

You could then restore it with a companion script.

---

## 🧩 7. Advanced: Declarative setups (optional)

If you want reproducibility **and** configurability long term, you might like:

- **Ansible**: automate package + config deployment (`xbps` supported)
    
- **chezmoi** or **yadm**: manage dotfiles across machines
    
- **Nix on Void** (yes, you can install Nix on Void): fully declarative user environments
    

---

## ✅ Summary

|Layer|How to reproduce|
|---|---|
|Packages|`xbps-query -l` → `xbps-install -S $(cat pkglist.txt)`|
|System config|`rsync /etc` or selective files|
|User config|dotfiles + `rsync` or `git`|
|Services (runit)|Copy `/etc/sv` + `/var/service`|
|Full automation|Script or Ansible|

---
**Two-script setup** for Void Linux that lets you **export** all your packages and configuration, then **restore** them on another machine.

They’re designed to be simple, transparent, and safe — no overwriting unless you confirm.

---

## 🧩 `void-export.sh` — create a portable backup

```bash
#!/bin/bash
# =======================================================
# Void Linux Backup Script
# Exports installed packages + system/user configuration
# =======================================================

set -euo pipefail

BACKUP_DIR="$HOME/void-backup-$(date +%F-%H%M)"
mkdir -p "$BACKUP_DIR"

echo "[+] Backup directory: $BACKUP_DIR"

# -------------------------------------------------------
# 1. Export package list
# -------------------------------------------------------
echo "[+] Exporting installed package list..."
xbps-query -l | awk '/ii/ {print $2}' > "$BACKUP_DIR/pkglist.txt"
echo "    -> Saved to $BACKUP_DIR/pkglist.txt"

# -------------------------------------------------------
# 2. Backup system configuration
# -------------------------------------------------------
echo "[+] Backing up key system config (/etc)..."
sudo rsync -aAX \
  --exclude='/etc/ssl' \
  --exclude='/etc/mtab' \
  --exclude='/etc/fstab' \
  --exclude='/etc/shadow' \
  /etc "$BACKUP_DIR/etc/"

# -------------------------------------------------------
# 3. Backup runit services
# -------------------------------------------------------
echo "[+] Backing up runit services..."
sudo rsync -aAX /etc/sv "$BACKUP_DIR/etc_sv/"
sudo rsync -aAX /var/service "$BACKUP_DIR/var_service/"

# -------------------------------------------------------
# 4. Backup user configuration
# -------------------------------------------------------
echo "[+] Backing up user configuration..."
rsync -aAX \
  --exclude='.cache' \
  --exclude='.local/share/Trash' \
  ~/.config "$BACKUP_DIR/home_config/"
cp -a ~/.bashrc ~/.zshrc ~/.profile "$BACKUP_DIR/home_config/" 2>/dev/null || true

# -------------------------------------------------------
# 5. Backup XBPS package cache (optional)
# -------------------------------------------------------
if [ -d /var/cache/xbps ]; then
    echo "[+] Copying local package cache..."
    sudo rsync -aAX /var/cache/xbps "$BACKUP_DIR/xbps_cache/"
fi

echo
echo "[✔] Backup completed successfully!"
echo "You can copy $BACKUP_DIR to your target machine."
```

---

## 🧩 `void-restore.sh` — restore your setup

```bash
#!/bin/bash
# =======================================================
# Void Linux Restore Script
# Installs packages + restores config and services
# =======================================================

set -euo pipefail

if [ -z "${1:-}" ]; then
  echo "Usage: sudo ./void-restore.sh /path/to/void-backup-YYYY-MM-DD-HHMM"
  exit 1
fi

BACKUP_DIR="$1"
if [ ! -d "$BACKUP_DIR" ]; then
  echo "Error: backup directory not found: $BACKUP_DIR"
  exit 1
fi

echo "[+] Using backup from: $BACKUP_DIR"
echo

# -------------------------------------------------------
# 1. Restore package list
# -------------------------------------------------------
if [ -f "$BACKUP_DIR/pkglist.txt" ]; then
  echo "[+] Installing packages from pkglist.txt..."
  xbps-install -S
  xbps-install -y $(cat "$BACKUP_DIR/pkglist.txt")
else
  echo "[!] No pkglist.txt found, skipping package install."
fi

# -------------------------------------------------------
# 2. Restore system configuration
# -------------------------------------------------------
read -p "[?] Restore /etc configuration files? (y/N): " CONFIRM
if [[ "$CONFIRM" =~ ^[Yy]$ ]]; then
  echo "[+] Restoring /etc configuration..."
  rsync -aAX "$BACKUP_DIR/etc/" /etc/
fi

# -------------------------------------------------------
# 3. Restore runit services
# -------------------------------------------------------
read -p "[?] Restore runit services? (y/N): " CONFIRM
if [[ "$CONFIRM" =~ ^[Yy]$ ]]; then
  echo "[+] Restoring runit service definitions..."
  rsync -aAX "$BACKUP_DIR/etc_sv/" /etc/sv/
  rsync -aAX "$BACKUP_DIR/var_service/" /var/service/
fi

# -------------------------------------------------------
# 4. Restore user configuration
# -------------------------------------------------------
echo "[+] Restoring user configuration..."
rsync -aAX "$BACKUP_DIR/home_config/" ~/

echo
echo "[✔] Restore completed!"
echo "You may need to restart services or log out/in."
```

---

## 🧩 How to use

### On the source machine

```bash
chmod +x void-export.sh
./void-export.sh
```

This creates a directory like:

```
~/void-backup-2025-10-30-1500/
```

### Copy to the new machine

```bash
rsync -av ~/void-backup-2025-10-30-1500 user@newhost:/home/user/
```

### On the target machine

```bash
chmod +x void-restore.sh
sudo ./void-restore.sh ~/void-backup-2025-10-30-1500
```

It’ll:

- Install the same packages (or latest versions)
    
- Restore configs (asks before overwriting `/etc`)
    
- Copy your dotfiles and `.config`
    

---

## 🧩 Optional improvements

- Add GPG signing or checksums for integrity.
    
- Use Git for your `home_config` directory for easier updates.
    
- Use `--repository=/path/to/xbps_cache` in restore if offline.
    
- Combine with `crontab` or `systemd` timer (Void uses `runit`) for automatic periodic backups.
    

---
