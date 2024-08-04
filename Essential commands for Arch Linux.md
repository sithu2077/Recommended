### System Update and Package Management

- **Update System**:
  ```bash
  sudo pacman -Syu
  ```
- **Install a Package**:
  ```bash
  sudo pacman -S [package_name]
  ```
- **Remove a Package**:
  ```bash
  sudo pacman -R [package_name]
  ```
- **Search for a Package**:
  ```bash
  pacman -Ss [search_term]
  ```
- **List Installed Packages**:
  ```bash
  pacman -Q
  ```

### System Information and Management

- **View System Information**:
  ```bash
  uname -a
  ```
- **Check Disk Usage**:
  ```bash
  df -h
  ```
- **Check Memory Usage**:
  ```bash
  free -h
  ```

### User and Permissions Management

- **Add a New User**:
  ```bash
  sudo useradd -m [username]
  ```
- **Set Password for User**:
  ```bash
  sudo passwd [username]
  ```
- **Add User to Group**:
  ```bash
  sudo usermod -aG [groupname] [username]
  ```

### System Services

- **Start a Service**:
  ```bash
  sudo systemctl start [service_name]
  ```
- **Enable a Service at Boot**:
  ```bash
  sudo systemctl enable [service_name]
  ```
- **Check Service Status**:
  ```bash
  systemctl status [service_name]
  ```

### File Management

- **Copy Files**:
  ```bash
  cp [source] [destination]
  ```
- **Move/Rename Files**:
  ```bash
  mv [source] [destination]
  ```
- **Remove Files**:
  ```bash
  rm [file_name]
  ```

### Network Management

- **Check Network Status**:
  ```bash
  ip a
  ```
- **Ping a Host**:
  ```bash
  ping [host]
  ```
- **Display Routing Table**:
  ```bash
  ip route
  ```

### Advanced Package Management

- **List Files Installed by a Package**:
  ```bash
  pacman -Ql [package_name]
  ```
- **Check Dependencies of a Package**:
  ```bash
  pacman -Qi [package_name]
  ```
- **Clean the Package Cache**:
  ```bash
  sudo pacman -Sc
  ```

### File Compression and Archiving

- **Extract a Tar Archive**:
  ```bash
  tar -xvf [archive.tar]
  ```
- **Create a Tar Archive**:
  ```bash
  tar -cvf [archive.tar] [directory]
  ```
- **Compress a File Using gzip**:
  ```bash
  gzip [file_name]
  ```
- **Decompress a gzip File**:
  ```bash
  gunzip [file_name.gz]
  ```

### Disk Management

- **List Block Devices**:
  ```bash
  lsblk
  ```
- **View Disk Partition Information**:
  ```bash
  fdisk -l
  ```
- **Mount a Filesystem**:
  ```bash
  sudo mount [device] [mount_point]
  ```
- **Unmount a Filesystem**:
  ```bash
  sudo umount [mount_point]
  ```

### Process Management

- **View Running Processes**:
  ```bash
  ps aux
  ```
- **Kill a Process by PID**:
  ```bash
  kill [PID]
  ```
- **Kill a Process by Name**:
  ```bash
  pkill [process_name]
  ```

### System Logs

- **View System Logs**:
  ```bash
  journalctl
  ```
- **View Boot Log**:
  ```bash
  journalctl -b
  ```

### Networking

- **View Active Network Connections**:
  ```bash
  netstat -tuln
  ```
- **Check Open Ports**:
  ```bash
  sudo lsof -i -P -n | grep LISTEN
  ```

### File Permissions

- **Change File Owner**:
  ```bash
  sudo chown [user]:[group] [file]
  ```
- **Change File Permissions**:
  ```bash
  chmod [permissions] [file]
  ```
- **Recursively Change Permissions**:
  ```bash
  chmod -R [permissions] [directory]
  ```

### SSH Commands

- **Connect to Remote Host via SSH**:
  ```bash
  ssh [user]@[host]
  ```
- **Copy Files Over SSH**:
  ```bash
  scp [file] [user]@[host]:[path]
  ```

### Time Management

- **Display Current Date and Time**:
  ```bash
  date
  ```
- **Set System Date and Time**:
  ```bash
  sudo date -s "YYYY-MM-DD HH:MM:SS"
  ```

### AUR (Arch User Repository) Helper Commands

- **Install a Package from AUR using Yay**:
  ```bash
  yay -S [package_name]
  ```
- **Update All AUR Packages**:
  ```bash
  yay -Syu
  ```

### More Package Management

- **Synchronize Package Databases**:
  ```bash
  sudo pacman -Sy
  ```
- **Upgrade Specific Package**:
  ```bash
  sudo pacman -S [package_name]
  ```
- **Remove Package and Unused Dependencies**:
  ```bash
  sudo pacman -Rns [package_name]
  ```

### Advanced File Management

- **Change File Owner Recursively**:
  ```bash
  sudo chown -R [user]:[group] [directory]
  ```
- **Create a Symbolic Link**:
  ```bash
  ln -s [target] [link_name]
  ```

### File Searching

- **Find Files by Name**:
  ```bash
  find /path/to/search -name [file_name]
  ```
- **Find Files by Type**:
  ```bash
  find /path/to/search -type [f/d] -name [file_name]
  ```
- **Search Inside Files**:
  ```bash
  grep -r [search_term] /path/to/search
  ```

### System Control and Management

- **Reboot System**:
  ```bash
  sudo reboot
  ```
- **Shutdown System**:
  ```bash
  sudo shutdown now
  ```
- **Power Off System**:
  ```bash
  sudo poweroff
  ```

### Networking and Security

- **Display IP Addresses**:
  ```bash
  ip addr show
  ```
- **Restart Network Service**:
  ```bash
  sudo systemctl restart NetworkManager
  ```
- **Flush DNS Cache**:
  ```bash
  sudo systemd-resolve --flush-caches
  ```

### Network Diagnostics

- **Traceroute to a Host**:
  ```bash
  traceroute [host]
  ```
- **Show DNS Information**:
  ```bash
  dig [domain]
  ```
- **Show WHOIS Information**:
  ```bash
  whois [domain]
  ```

### Advanced Disk Management

- **Create a Filesystem**:
  ```bash
  sudo mkfs.ext4 [device]
  ```
- **Check and Repair Filesystem**:
  ```bash
  sudo fsck [device]
  ```

### User Management

- **List All Users**:
  ```bash
  cut -d: -f1 /etc/passwd
  ```
- **List All Groups**:
  ```bash
  cut -d: -f1 /etc/group
  ```
- **Delete a User**:
  ```bash
  sudo userdel [username]
  ```
- **Change User's Default Shell**:
  ```bash
  sudo chsh -s /bin/bash [username]
  ```

### Arch Linux Specific Tools

- **View System Logs with journalctl**:
  ```bash
  journalctl -xe
  ```
- **Update Mirrors**:
  ```bash
  sudo pacman-mirrors -g
  ```

### AUR (Arch User Repository) Helper Commands (Continued)

- **Search for a Package in AUR using Yay**:
  ```bash
  yay -Ss [search_term]
  ```
- **Remove Unused Dependencies with Yay**:
  ```bash
  yay -Yc
  ```

### Customizing and Configuring System

- **Edit GRUB Configuration**:
  ```bash
  sudo nano /etc/default/grub
  sudo grub-mkconfig -o /boot/grub/grub.cfg
  ```
- **Enable Multilib Repository**:
  ```bash
  sudo nano /etc/pacman.conf
  ```
  Add the following lines:
  ```
  [multilib]
  Include = /etc/pacman.d/mirrorlist
  ```
  Then run:
  ```bash
  sudo pacman -Sy
  ```

### System Monitoring

- **Real-Time System Monitoring with top**:
  ```bash
  top
  ```
- **Real-Time System Monitoring with htop**:
  ```bash
  htop
  ```
- **View Disk I/O**:
  ```bash
  iotop
  ```

### Advanced System Information

- **View CPU Information**:
  ```bash
  lscpu
  ```
- **View Detailed Hardware Information**:
  ```bash
  lshw
  ```
- **List PCI Devices**:
  ```bash
  lspci
  ```
- **List USB Devices**:
  ```bash
  lsusb
  ```

### Advanced Networking

- **Display Routing Table**:
  ```bash
  route -n
  ```
- **Network Interface Statistics**:
  ```bash
  ifconfig
  ```
- **Manage Firewall with UFW**:
  - Enable UFW:
    ```bash
    sudo ufw enable
    ```
  - Allow Port:
    ```bash
    sudo ufw allow [port_number]
    ```
  - Deny Port:
    ```bash
    sudo ufw deny [port_number]
    ```
  - Check UFW Status:
    ```bash
    sudo ufw status
    ```

### Disk and Partition Management

- **List Mounted Filesystems**:
  ```bash
  mount | column -t
  ```
- **Resize a Filesystem**:
  ```bash
  sudo resize2fs [device]
  ```
- **Create a New Partition Table**:
  ```bash
  sudo parted [device] mklabel [label_type]
  ```
- **Create a New Partition**:
  ```bash
  sudo parted [device] mkpart [partition_name] [file_system_type] [start] [end]
  ```

### Advanced File Manipulation

- **Change File Attributes**:
  ```bash
  chattr +[attribute] [file]
  ```
- **List File Attributes**:
  ```bash
  lsattr [file]
  ```

### Software Development Tools

- **Compile and Install Software from Source**:
  ```bash
  ./configure
  make
  sudo make install
  ```
- **Install Development Tools Group**:
  ```bash
  sudo pacman -S base-devel
  ```

### System Backup and Restore

- **Backup Files Using rsync**:
  ```bash
  rsync -av --progress [source] [destination]
  ```
- **Create a Disk Image with dd**:
  ```bash
  sudo dd if=[input_file] of=[output_file] bs=4M
  ```
- **Restore from a Disk Image with dd**:
  ```bash
  sudo dd if=[image_file] of=[device] bs=4M
  ```

### Managing Snapshots with Btrfs

- **Create a Btrfs Snapshot**:
  ```bash
  sudo btrfs subvolume snapshot [source] [destination]
  ```
- **List Btrfs Snapshots**:
  ```bash
  sudo btrfs subvolume list /
  ```

### System Maintenance

- **Check for Broken Symlinks**:
  ```bash
  find / -xtype l
  ```
- **Clean Package Cache**:
  ```bash
  sudo pacman -Scc
  ```
- **Check for Orphaned Packages**:
  ```bash
  sudo pacman -Qdt
  ```

### Automating Tasks with Cron

- **Edit Crontab**:
  ```bash
  crontab -e
  ```
- **List Crontab Jobs**:
  ```bash
  crontab -l
  ```

### Security and Encryption

- **Encrypt a File with GPG**:
  ```bash
  gpg -c [file]
  ```
- **Decrypt a File with GPG**:
  ```bash
  gpg [file.gpg]
  ```
- **Set Up SSH Key Authentication**:
  - Generate SSH Key Pair:
    ```bash
    ssh-keygen -t rsa -b 4096
    ```
  - Copy Public Key to Remote Host:
    ```bash
    ssh-copy-id [user]@[host]
    ```

### Virtualization and Containers

- **Install Docker**:
  ```bash
  sudo pacman -S docker
  ```
  - Start Docker Service:
    ```bash
    sudo systemctl start docker
    sudo systemctl enable docker
    ```
  - Run a Docker Container:
    ```bash
    sudo docker run [image_name]
    ```

### Miscellaneous Useful Commands

- **Generate a Random Password**:
  ```bash
  openssl rand -base64 12
  ```
- **Download a File with wget**:
  ```bash
  wget [url]
  ```
- **Download a File with curl**:
  ```bash
  curl -O [url]
  ```

### System Monitoring and Performance

- **Monitor Network Usage**:
  ```bash
  nload
  ```
- **View Memory Usage**:
  ```bash
  vmstat
  ```
- **Display CPU Information**:
  ```bash
  lscpu
  ```
- **Show Detailed Disk Usage**:
  ```bash
  du -h --max-depth=1
  ```

### Advanced Networking

- **Set Static IP Address**:
  Edit the network configuration file, typically found at `/etc/netctl/`:
  ```bash
  sudo nano /etc/netctl/[profile_name]
  ```
  Add/Edit:
  ```bash
  IP=static
  Address=('192.168.1.100/24')
  Gateway='192.168.1.1'
  DNS=('8.8.8.8' '8.8.4.4')
  ```
  Then restart the network:
  ```bash
  sudo netctl restart [profile_name]
  ```
- **Check Network Interfaces**:
  ```bash
  ifconfig -a
  ```

### Arch User Repository (AUR) with More Helpers

- **Install Trizen (AUR Helper)**:
  ```bash
  git clone https://aur.archlinux.org/trizen.git
  cd trizen
  makepkg -si
  ```
- **Install a Package Using Trizen**:
  ```bash
  trizen -S [package_name]
  ```

### Backup and Restore

- **Create a Backup of a Directory**:
  ```bash
  tar -czvf backup.tar.gz /path/to/directory
  ```
- **Extract a Backup**:
  ```bash
  tar -xzvf backup.tar.gz
  ```
- **Create a Disk Image**:
  ```bash
  dd if=/dev/sdX of=/path/to/backup.img
  ```
- **Restore a Disk Image**:
  ```bash
  dd if=/path/to/backup.img of=/dev/sdX
  ```

### Compiling and Installing from Source

- **Download Source Code**:
  ```bash
  git clone [repository_url]
  ```
- **Navigate to Source Directory**:
  ```bash
  cd [source_directory]
  ```
- **Compile and Install**:
  ```bash
  ./configure
  make
  sudo make install
  ```

### Managing Systemd Services

- **List All Services**:
  ```bash
  systemctl list-units --type=service
  ```
- **Stop a Service**:
  ```bash
  sudo systemctl stop [service_name]
  ```
- **Disable a Service**:
  ```bash
  sudo systemctl disable [service_name]
  ```

### Kernel Management

- **List Installed Kernels**:
  ```bash
  sudo pacman -Q | grep linux
  ```
- **Install a New Kernel**:
  ```bash
  sudo pacman -S linux-zen
  ```
- **Remove an Old Kernel**:
  ```bash
  sudo pacman -R linux-oldversion
  ```

### Hardware Management

- **List PCI Devices**:
  ```bash
  lspci
  ```
- **List USB Devices**:
  ```bash
  lsusb
  ```
- **Display Detailed Hardware Information**:
  ```bash
  lshw
  ```

### Using Makepkg

- **Build a Package from PKGBUILD**:
  ```bash
  makepkg -si
  ```
- **Install Dependencies from PKGBUILD**:
  ```bash
  makepkg -s
  ```
- **Clean Build Directory**:
  ```bash
  makepkg -c
  ```

### System Configuration and Customization

- **Edit Hosts File**:
  ```bash
  sudo nano /etc/hosts
  ```
- **Edit Resolv.conf for DNS**:
  ```bash
  sudo nano /etc/resolv.conf
  ```
- **Configure Locale Settings**:
  ```bash
  sudo nano /etc/locale.gen
  sudo locale-gen
  ```

### Automation and Scheduling

- **List Crontab Entries**:
  ```bash
  crontab -l
  ```
- **Edit Crontab Entries**:
  ```bash
  crontab -e
  ```
- **Schedule a Task with Systemd Timer**:
  Create a `.service` file in `/etc/systemd/system/`:
  ```bash
  sudo nano /etc/systemd/system/[your_task].service
  ```
  Example content:
  ```bash
  [Unit]
  Description=My Scheduled Task

  [Service]
  ExecStart=/path/to/script.sh
  ```
  Create a `.timer` file in the same directory:
  ```bash
  sudo nano /etc/systemd/system/[your_task].timer
  ```
  Example content:
  ```bash
  [Unit]
  Description=Run My Scheduled Task every hour

  [Timer]
  OnCalendar=hourly
  Persistent=true

  [Install]
  WantedBy=timers.target
  ```
  Enable the timer:
  ```bash
  sudo systemctl enable --now [your_task].timer
  ```

### System Maintenance

- **Clear Package Cache**:
  ```bash
  sudo pacman -Scc
  ```
- **Remove Orphaned Packages**:
  ```bash
  sudo pacman -Rns $(pacman -Qtdq)
  ```

### Logs and Diagnostics

- **Show Boot Messages**:
  ```bash
  dmesg
  ```
- **Display Last System Boot Time**:
  ```bash
  who -b
  ```
- **Show Last System Reboots**:
  ```bash
  last reboot
  ```

### Advanced User Management

- **Lock a User Account**:
  ```bash
  sudo usermod -L [username]
  ```
- **Unlock a User Account**:
  ```bash
  sudo usermod -U [username]
  ```

### Advanced Networking

- **Display Routing Table**:
  ```bash
  route -n
  ```
- **Configure Network Interfaces**:
  ```bash
  sudo nano /etc/netctl/[profile_name]
  sudo netctl restart [profile_name]
  ```
- **View ARP Cache**:
  ```bash
  arp -a
  ```

### Firewall Management

- **Install UFW (Uncomplicated Firewall)**:
  ```bash
  sudo pacman -S ufw
  ```
- **Enable UFW**:
  ```bash
  sudo ufw enable
  ```
- **Allow a Port through UFW**:
  ```bash
  sudo ufw allow [port_number]
  ```
- **Check UFW Status**:
  ```bash
  sudo ufw status
  ```

### More Advanced Disk Management

- **Create and Mount Swap File**:
  ```bash
  sudo fallocate -l 2G /swapfile
  sudo chmod 600 /swapfile
  sudo mkswap /swapfile
  sudo swapon /swapfile
  echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
  ```
- **Resize Filesystem**:
  ```bash
  sudo resize2fs /dev/sdXn
  ```

### Advanced Process Management

- **Show Top Memory-Consuming Processes**:
  ```bash
  ps aux --sort=-%mem | head
  ```
- **Show Top CPU-Consuming Processes**:
  ```bash
  ps aux --sort=-%cpu | head
  ```

### Snapshots and Backups with Btrfs

- **Create a Btrfs Subvolume**:
  ```bash
  sudo btrfs subvolume create /mnt/@subvolume
  ```
- **List Btrfs Subvolumes**:
  ```bash
  sudo btrfs subvolume list /mnt
  ```
- **Create a Snapshot**:
  ```bash
  sudo btrfs subvolume snapshot /mnt/@subvolume /mnt/@snapshot
  ```

### LVM (Logical Volume Management)

- **Create a Physical Volume**:
  ```bash
  sudo pvcreate /dev/sdX
  ```
- **Create a Volume Group**:
  ```bash
  sudo vgcreate [volume_group_name] /dev/sdX
  ```
- **Create a Logical Volume**:
  ```bash
  sudo lvcreate -n [logical_volume_name] -L [size] [volume_group_name]
  ```

### More Advanced AUR Usage

- **Rebuild All AUR Packages**:
  ```bash
  yay -S --rebuildall $(yay -Qm | awk '{print $1}')
  ```

### Power Management

- **Suspend System**:
  ```bash
  sudo systemctl suspend
  ```
- **Hibernate System**:
  ```bash
  sudo systemctl hibernate
  ```
- **Hybrid Sleep (Suspend and Hibernate)**:
  ```bash
  sudo systemctl hybrid-sleep
  ```

### Customizing the Bootloader

- **Edit GRUB Configuration**:
  ```bash
  sudo nano /etc/default/grub
  sudo grub-mkconfig -o /boot/grub/grub.cfg
  ```
- **Install GRUB Bootloader**:
  ```bash
  sudo grub-install /dev/sdX
  ```

### Using Systemd for Power Management

- **Poweroff the System**:
  ```bash
  sudo systemctl poweroff
  ```
- **Restart the System**:
  ```bash
  sudo systemctl reboot
  ```
- **Suspend to RAM**:
  ```bash
  sudo systemctl suspend
  ```

### Managing Kernel Modules

- **List Loaded Kernel Modules**:
  ```bash
  lsmod
  ```
- **Load a Kernel Module**:
  ```bash
  sudo modprobe [module_name]
  ```
- **Unload a Kernel Module**:
  ```bash
  sudo modprobe -r [module_name]
  ```

### Using Arch-Chroot

- **Enter Chroot Environment**:
  ```bash
  sudo arch-chroot /mnt
  ```

### More Disk Encryption with LUKS

- **Encrypt a Disk Partition**:
  ```bash
  sudo cryptsetup luksFormat /dev/sdX
  ```
- **Open Encrypted Partition**:
  ```bash
  sudo cryptsetup open /dev/sdX [name]
  ```
- **Close Encrypted Partition**:
  ```bash
  sudo cryptsetup close [name]
  ```

### Building and Installing Custom Kernels

- **Install Required Packages**:
  ```bash
  sudo pacman -S base-devel linux-headers
  ```
- **Download Kernel Source**:
  ```bash
  wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.x.tar.xz
  tar -xvf linux-5.x.tar.xz
  ```
- **Configure Kernel**:
  ```bash
  cd linux-5.x
  make menuconfig
  ```
- **Compile and Install Kernel**:
  ```bash
  make
  sudo make modules_install
  sudo make install
  ```
