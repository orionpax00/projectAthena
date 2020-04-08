## ARCH Installation with couple of different things

### Requirements:
* computer
* internet
* USB drive


### Steps:
#### Steps in the host computer(in which you are not going to install OS)
* List all available drive on the system 
  ```bash
  lsblk
  ```
* Attach USB drive and distinguise between attached drive and available drive using ***lsblk*** command. And Remember that
* Enable root user
  ```bash
  sudo su
  ```
* Use ***dd*** command for formatting and uploading downloaded iso to the USB
  ```bash
  dd if=<location of iso> of=<location of attached usb> status="progress"
  ```
* Check for UFEI or Traditional BIOS, What your system have
  ```bash
  yet to add
  ```
* Partitioning of disk 
  ```
  fdisk <location of disk>
  ```
  After running the above command new command prompt will start uses below command to start partitioning.
  ```
  Command : p //delete any partition disk have
  Command: d //if more than 1 partition run it couple of time
  // do partitioning
  Command: n // for creating new partition 
  //Create 4 partition
  --> /dev/sda1 : boot partition // 200mb // for grub menu
  --> /dev/sda2 : swap partition // 12-16gb // herbernation related to the RAM
  --> /dev/sda3 : root partition // 25gb // for software 
  --> /dev/sda4 : home partition // remaining disk space // for user related files
  Command: w // write changes, it will wipe everthing that perviously has on disk
  ```
* Make file systems
  ```
  mkfs.ext4 /dev/sda1
  mkfs.ext4 /dev/sda3
  mkfs.ext4 /dev/sda4

  // swap partition will not have any file system
  ```
* Setup Swap partition
  ```
  mkswap /dev/sda2
  swapon /dev/sda2
  ```
* Mount file
  ```
  mount /dev/sda3 /
  mount /dev/sda4 /home
  mount /dev/sda1 /boot

  // you are on a actual install use
  mount /dev/sda3 /mnt
  mkdir /mnt/boot /mnt/home
  mount /dev/sda1 /mnt/boot
  mount /dev/sda4 /mnt/home
  ```
* Install base arch linux
  ```
  pacstrap <location where you want to install arch like / or /mnt> base base-devel vim
  ```
* fstab file: to remember mount point and partitions
  ```
  genfstab -U <location of drive with partition like / or /mnt> >> /etc/fstab
  ```
* Change root(chroot): move into the actual installation
  ```
  arch-chroot <location of arch install / or /mnt>
  ```
* Actual installation are going from here
* Install network manager
  ```
  pacman -S networkmanager
  ```
* Make Network Manager a service
  ```
  systemctl enable networkManager
  ```
* Installing grub
  ```
  pacman -S grub
  ```
* Generating Grub Configuration
  ```
  grub-install --target=i386-pc /dev/sda
  grub-mkconfig -o /boot/grub/grub.cfg
  ```
* Setup Password
  ```
  passwd //root password
  ```
* Setting up Local
  ```
  vim /etc/locale.gen // uncomment your locale
  locale-gen
  vim /etc/locale.conf
  // add these lines
  LANG=en-US.UTF-8 
  ```
* Setting up Time Zone
  ```
  ls /usr/share/zoneinfo/
  ln -sf /usr/share/zoneinfo/<your location>/<your location> /etc/localtime
  ```
* setting up hostname
  ```
  vim /etc/hostname
  //add these line
  name_of_your_compute //like mylaptop,etc
  ```
* Exit from the installation, and un-mount everything i.e drive
  ```
  exit
  umount -R /mnt // will not be required
  ```
* Reboot
  ```
  reboot
  ```

Now your system will have running Arch Linux with tty mode ping for internet and check connection.
\
Now its time to install Desktop Environment.

#### Installing Desktop Environment
* Create User
  ```
  useradd -m -g wheel <username>
  passwd <username>
  ```
* Give Sudo permission to the user
  ```
  vim /etc/sudoers
  //uncomment this lines
  root ALL=(ALL) ALL
  ```
* Install any Desktop Environment like XFCE, Gnome, KDE, etc
  ```
  pacman -S xfce4
  ``` 
* Create ~/.xinitrc
  ```
  vim ~/.xinitrc
  //add these lines
  exec xfce4-session
  ```
  ##### From here it will be dwm and i3 centeric Installation.
* List of things to install with Window Manager
  * X-org
  * Terminal Emulator
  * Window Manager(i3, dwm, bspwm, awesome, etc)

* Install Xorg
  ```
  pacman -S xorg xorg-server xinit
  ```
* Install i3WM and terminal emulator
  ```
  pacman -S i3-gaps i3-status dmenu urxvt
  ```
* Install Fonts
  ```
  pacman -S noto-font
  //setup font manually if fonts have some problem
  ~/.config/fontconfig/fonts.conf // it is an xml file
  ```
* Install Network Manager (nm-applet)

* Create ~/.xinitrc
  ```
  vim ~/.xinitrc
  //add these lines
  exec i3wm
  ```
* User Specific Settings ~/.profile
  ```vim ~/.profile
  //add what you wnat like
  ```

### FAQs
**startx doesn't run**  
Download video driver \
pacman -S x86-video-intel





