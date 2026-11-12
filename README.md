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

Bootloader >> Unified kernel images >> No >> Back

Authentication >> User account >> Add a user >> *Your username* >> *Your password* >> *Confirm password* >> Yes >> Confirm and exit >> Back

Network configuration >> Use Network Manager (default backend)

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

`sudo pacman-key --recv-keys F3B607488DB35A47 --keyserver keyserver.ubuntu.com; sudo pacman-key --lsign-key F3B607488DB35A47; sudo pacman -U 'https://mirror.cachyos.org/repo/x86_64/cachyos/cachyos-keyring-20240331-1-any.pkg.tar.zst'; sudo pacman -U 'https://mirror.cachyos.org/repo/x86_64/cachyos/cachyos-mirrorlist-27-1-any.pkg.tar.zst'`

Root paste settings folders now.

`sudo pacman -Syu`

`sudo pacman -S brave-origin-bin cosmic-text-editor cpupower gamemode linux-cachyos-eac mission-center obs-studio octopi papirus-icon-theme photocraft protonplus scx-tools signal-desktop steam systemd-boot-cachyos-signed xdg-user-dirs`

Nvidia GPU `sudo pacman -S linux-cachyos-eac-nvidia-open`

Framework `sudo pacman -S framework-system`

`systemctl enable cpupower; systemctl enable scx_loader`

Reboot.

`sudo pacman -Syyuu; sudo pacman -Scc --noconfirm; pacman -Qqd | sudo pacman -Rsu - `

# Credit
* The Arch Wiki && CachyOS Devs for various configs
