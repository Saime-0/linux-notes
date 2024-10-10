Connect to wifi 

- exec cmd `iwctl` to enter in interactive mode
- exec cmd `station <wlan-name> scan` for start scanning
- exec cmd `station <wlan> connect <network>` for connect to network
- enter password
- ctrl+d

Partiotioning disk

- exec cmd `parted /dev/sda` to enter in interactiove mode (replace *sda* with your need device)
- exec cmd `mklabel gpt` for create gpt
- exec cmd `mkpart ESP fat32 1MiB 900MiB` for create boot part (named /dev/sda1 in later)
- exec cmd `set 1 boot on` fot set boot flag to part
- exec cmd `mkpart primary ext4 900MiB 100%` for create part will using lvm (named /dev/sda2 in later)
- exec cmd `quit`

Setup LVM

- exec cmd `pvcreate /dev/sda2` for create a physical volume
- exec cmd `vgcreate avg0 /dev/sda2` for create volume group
- exec cmd `lvcreate -L 60G avg0 -n root` for create logical volume for root part
- exec cmd `lvcreate -L 8G avg0 -n swap` for create logical volume for root part
- exec cmd `lvcreate -l 100%FREE avg0 -n home` for create logical volume for root part
- exec cmd `lvreduce -L -256M avg0/home` for leave at least 256 MiB free space in the volume group to allow using e2scrub(8) ([arch guide tip](https://wiki.archlinux.org/title/Install_Arch_Linux_on_LVM#Create_logical_volumes))

Format the partitions

- exec cmd `mkfs.fat -F32 /dev/sda1` formatting boot volume
- exec cmd `mkfs.ext4 /dev/avg0/root` formatting root volume
- exec cmd `mkfs.ext4 /dev/avg0/home` formatting home volume
- exec cmd `mkswap /dev/avg0/swap` formatting swap volume
- exec cmd `swapon /dev/avg0/swap` enable swap

Mount fs

- exec cmd `mount --mkdir /dev/avg0/root mnt`
- exec cmd `mount --mkdir /dev/avg0/home mnt/home`
- exec cmd `mount --mkdir /dev/sda1 mnt/boot`

Install system to mounted fs

- exec cmd `pacstrap -K mnt base linux linux-firmware bash-completion vim iwd wpa_supplicant lvm2`
- exec cmd `genfstab -U mnt >> mnt/etc/fstab`
- exec cmd `arch-chroot mnt` for enter

Setup mounted fs

- uncomment in `/etc/locale.gen` file needed localisations: `en_US.UTF-8 UTF-8` and `ru_RU.UTF-8 UTF-8`
- exec cmd `locale-gen` for generate locales
- exec `echo "LANG=en_US.UTF-8" > /etc/locale.conf`
- exec cmd `ln -sf /usr/share/zoneinfo/Europe/Moscow /etc/localtime` for set TZ
- exec cmd `hwclock --systohc`
- edit `/etc/mkinitcpio.conf` file - insert `lvm2` between `block` and `filesystems` like so: `HOOKS="base udev ... block lvm2 filesystems"` to provide support for lvm2
- exec `mkinitcpio -p linux` for generate the initramfs image
- exec `passwd` and enter password for root

Setup boot

- `bootctl install`
- edit `/boot/loader/loader.conf`
```
default  arch
timeout  4
editor   0
```
- edit `/boot/loader/entries/arch-lvm.conf` for creating entry
```
title          Arch Linux (LVM)
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=/dev/mapper/avg0-root rw
```

Exit from install

- Ctrl + D
- exec  cmd `umount -R mnt`
- exec cmd `reboot`


### Used resources

arch Installation guide - https://wiki.archlinux.org/title/Installation_guide

install arch on lvm - https://wiki.archlinux.org/title/Install_Arch_Linux_on_LVM

gist Installing Arch with LVM - https://gist.github.com/KarthikNayak/912c268aa62c3ede3c0f707164f2d4ab
