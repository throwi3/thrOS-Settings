System install /w archinstall.

## Pre-archinstall Setup

Using your ISO flasher of choice (I personally like using the [Fedora Media Writer](https://www.fedoraproject.org/workstation/download/#fedora-media-writer) for linux ISOs), flash a base [Arch Linux ISO](https://archlinux.org/download/) to a usb flash drive.

Boot from the drive in your boot/UEFI menu. Check your motherboards manual if you do not know how to do this for your system.

Connecting to the internet for Ethernet users should be automatic. Wifi users will need to follow the following steps. 

`iwctl`

`station wlan0 scan`

`station wlan0 connect *Your SSID*`

*Enter password*

`exit`

Go to https://wiki.archlinux.org/title/Iwd if you need more info.

Run `archinstall` to open archinstall.

## archinstall Setup

Mirrors and repositories >> Select regions >> *Your Country* with space >> Optional repositories >> multilib with space >> Back

Disk configuration >> Partitioning >> Use a best-effort default partition layout >> *Your Boot Disk* >> btrfs >> Yes >> Use compression >> Back

Bootloader >> Bootloader >> Limine >> Unified kernel images >> No >> Back

Kernels >> Deselect "linux" with space >> Select "linux-zen" with space

Authentication >> User account >> Add a user >> *Your username* >> *Your password* >> *Confirm password* >> Yes >> Confirm and exit >> Back

Network configuration >> Use Network Manager (iwd backend)

Timezone >> *Select your timezone*

Install

Yes

**Enjoy the ride for a moment.**

chroot into installation for post-installation configurations

`sudo pacman -S cosmic-session cosmic-terminal firefox ly nemo-fileroller`

`systemctl enable ly@tty1.service; systemctl disable getty@tty1.service`

`exit`

`reboot`

## Post archinstall Setup

`sudo pacman-key --recv-key 3056513887B78AEB --keyserver keyserver.ubuntu.com; sudo pacman-key --lsign-key 3056513887B78AEB; sudo pacman -U 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-keyring.pkg.tar.zst'; sudo pacman -U 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-mirrorlist.pkg.tar.zst'`

Root paste settings folders now.

`sudo pacman -Syu`

Nvidia GPU `sudo pacman -S linux-zen-headers nvidia-open-dkms`

Framework `sudo pacman -S framework-system`

`sudo pacman -S brave-origin-bin cosmic-text-editor cpupower gamemode limine-mkinitcpio-hook mission-center noto-color-emoji-fontconfig noto-fonts-cjk obs-pipewire-audio-capture obs-studio-tytan652 octopi papirus-icon-theme photocraft protonplus scx-tools signal-desktop steam xdg-user-dirs`

`systemctl enable cpupower; systemctl enable scx_loader`

Reboot.

`sudo pacman -Syyuu; sudo pacman -Scc --noconfirm; pacman -Qqd | sudo pacman -Rsu - `

# Credit
* The Arch Wiki && CachyOS Devs for various configs
