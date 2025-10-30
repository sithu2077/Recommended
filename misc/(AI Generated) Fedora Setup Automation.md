**Automate your Fedora setup** using a combination of configuration management tools, package lists, and dotfiles - Here’s a clear step-by-step guide (with multiple automation options) to replicate your old Fedora laptop on a new one.

---

## 🧭 Step 1. Document or Export Your Current Setup

On your **current Fedora laptop**, collect:

1. **Installed packages**
    
    ```bash
    sudo dnf list installed > ~/dnf-packages.txt
    ```
    
    or more compactly:
    
    ```bash
    rpm -qa --qf '%{NAME}\n' > ~/packages.txt
    ```
    
2. **Flatpak apps**
    
    ```bash
    flatpak list --app --columns=application > ~/flatpak-apps.txt
    ```
    
3. **Shell config files and dotfiles**  
    Backup:
    
    ```bash
    mkdir ~/fedora-backup
    cp -r ~/.bashrc ~/.zshrc ~/.config ~/.local/share/fonts ~/.ssh ~/.gitconfig ~/fedora-backup/
    ```
    
4. (Optional) **GNOME extensions and settings**
    
    ```bash
    gnome-extensions list --enabled > ~/enabled-extensions.txt
    dconf dump / > ~/dconf-settings.ini
    ```
    
5. Store all this in a Git repo or cloud folder (e.g., GitHub, GitLab, or private drive).
    

---

## ⚙️ Step 2. Choose an Automation Method

You have three main options:

### 🅰️ Option 1. Use a Setup Script (Simplest)

Create a shell script (`setup-fedora.sh`) that:

- Updates the system
    
- Installs packages from your saved list
    
- Restores config files and settings
    

Example:

```bash
#!/usr/bin/env bash
set -e

echo "Updating system..."
sudo dnf update -y

echo "Installing packages..."
xargs sudo dnf install -y < packages.txt

echo "Installing Flatpaks..."
xargs -I {} flatpak install -y flathub {}

echo "Restoring configs..."
cp -r ~/fedora-backup/.* ~/
dconf load / < ~/fedora-backup/dconf-settings.ini

echo "Setup complete!"
```

Run this on your new laptop:

```bash
chmod +x setup-fedora.sh
./setup-fedora.sh
```

---

### 🅱️ Option 2. Use **Ansible** (More powerful & repeatable)

1. On your old laptop, install Ansible:
    
    ```bash
    sudo dnf install ansible -y
    ```
    
2. Create a playbook (`fedora-setup.yml`):
    
    ```yaml
    - hosts: localhost
      become: true
      tasks:
        - name: Update system
          dnf:
            name: "*"
            state: latest
    
        - name: Install packages
          dnf:
            name: "{{ lookup('file', 'packages.txt').splitlines() }}"
            state: present
    
        - name: Install Flatpaks
          command: flatpak install -y flathub {{ item }}
          loop: "{{ lookup('file', 'flatpak-apps.txt').splitlines() }}"
          ignore_errors: yes
    
        - name: Copy config files
          copy:
            src: /path/to/your/dotfiles/
            dest: /home/{{ ansible_user }}/
            owner: "{{ ansible_user }}"
            mode: preserve
    ```
    
3. Save your playbook and config files in a Git repo.
    
4. On the new laptop:
    
    ```bash
    sudo dnf install ansible -y
    git clone <your_repo>
    cd <your_repo>
    ansible-playbook fedora-setup.yml
    ```
    

---

### 🅾️ Option 3. Use **Fedora Kickstart** (for full OS install automation)

If you want to automate the _entire OS installation_ (not just after it’s installed):

- Export your current kickstart config:
    
    ```bash
    sudo anaconda --dumpconfig=custom.ks
    ```
    
- Edit `custom.ks` to add post-install steps (package installs, copying configs).
    
- Use it when installing Fedora (boot the installer with `inst.ks=<path>`).
    

---

## ☁️ Step 3. Keep It in Version Control

Store your:

- setup script / playbook
    
- dotfiles
    
- package lists
    

in a **GitHub repo**, so next time you just run:

```bash
git clone https://github.com/<yourusername>/fedora-setup.git
cd fedora-setup
./setup-fedora.sh
```

or

```bash
ansible-playbook fedora-setup.yml
```

---

## 💡 Optional Enhancements

- Use **chezmoi** or **dotbot** for dotfile management.
    
- Use **Homebrew** on Fedora for some cross-platform dev tools.
    
- Store secrets (e.g., SSH keys) encrypted with `gpg` or `ansible-vault`.
    

---
