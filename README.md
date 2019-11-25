# wos
Wos
```bash
ping archlinux.org
timedatectl set-ntp true
fdisk -l
fdisk /dev/sdX
mkfs.fat -F 32 /dev/sdX1
mkswap /dev/sdX2
swapon /dev/sdX2
mkfs.ext4 /dev/sdX3
mkfs.ext4 /dev/sdX4
mount /dev/sdX3 /mnt
mkdir /mnt/boot
mkdir /mnt/home
mount /dev/sdX1 /mnt/boot
mount /dev/sdX4 /mnt/home
pacstrap /mnt base linux linux-firmware gvim
genfstab -U /mnt >> /mnt/etc/fstab
arch-chroot /mnt
ln -sf /usr/share/zoneinfo/Region/City /etc/localtime
hwclock --systohc
vim /etc/locale.gen
locale-gen
/etc/locale.conf
---
LANG=en_US.UTF-8
---

vim /etc/hostname
---
myhostname
---

vim /etc/hosts
---
127.0.0.1	localhost
::1		localhost
127.0.1.1	myhostname.localdomain	myhostname
---

passwd
pacman -Syu
pacman -S gnome gnome-flashback gnome-keyring gnome-tweaks gnome-applets xf86-video-fbdev xorg-server xorg-xinit network-manager-applet ttf-dejavu ttf-droid xmonad xmonad-contribi dmenu
pacman -S intel-ucode amd-ucode
grub-install --target=i386-pc /dev/sdX
grub-mkconfig -o /boot/grub/grub.cfg
reboot
useradd -m -G users -s /bin/bash user
passwd user
systemctl start gdm.service
systemctl enable NetworkManager.service
pacman -S sudo
vim /etc/sudoers
---
## Uncomment to allow members of group wheel to execute any command
%wheel ALL=(ALL) ALL
---

pacman -Rs gnome-software gnome-music
pacman -S ntfs-3g android-file-transfer chromium vlc libreoffice-fresh gimp git clipgrap
pacman -S android-tools android-udev
cp /etc/X11/xinit/xinitrc ~/.xinitrc
vim ~/.xinitrc
---
...
exec xmonad
---

mkdir .xmonad
vim .xmonad/xmonad.hs
---
import XMonad

main = xmonad def
    { terminal    = "urxvt"
    , modMask     = mod4Mask
    , borderWidth = 3
    }
---

xmonad --recompile
```
