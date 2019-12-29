 ###### General Installation procedure (standard install on EFI) in "01/01/2020":
`# cfdisk /dev/sda` then make partitions.
`# mkfs.fat -F32 /dev/sda1` Skip if already had EFI partition.
`# mkswap /dev/sda4` then `swapon /dev/sda4`
`# mkfs.ext4 /dev/sda5`
`# mkfs.ext4 /dev/sda6`
`# mount /dev/sda6 /mnt`
`# mkdir /mnt/home`
`# mount /dev/sda5 /mnt/home`
`# mkdir /mnt/boot`
`# mount /dev/sda1 /mnt/boot`
`# pacstrap /mnt base base-devel linux linux-firmware linux-headers`
`# genfstab -U /mnt >> /mnt/etc/fstab`
`# arch-chroot /mnt`
`# passwd` root passwd
`# pacman -S vim networkmanager` then enable NetworkManager.service
`# useradd -m -g users -G wheel,storage,power,video,audio -s /bin/bash sentaku` then `# passwd sentaku`
`# EDITOR=vim visudo`. and uncomment : %wheel ALL=(ALL) ALL
`# vim /etc/locale.gen` (uncomment en_US.UTF-8)
`# locale-gen`
`# echo LANG=en_US.UTF-8 > /etc/locale.conf`
`# export LANG=en_US.UTF-8`
`# ln -sf /usr/share/zoneinfo/Africa/Algiers /etc/localtime`
`# hwclock --systohc`
`# echo X1C-Pro > /etc/hostname`
`# mkinitcpio -P`
  ######Instaling EFISTUB boot loader #####
`# pacman -S fuse intel-ucode ntfs-3g efibootmgr`
`# efibootmgr --disk /dev/sda1 --part 1 --create --label "Arch Linux" --loader /vmlinuz-linux --unicode 'root=PARTUUID=ForRoot quiet loglevel=3 rd.systemd.show_status=auto rd.udev.log_priority=3 rw resume=PARTUUID=ForSwap initrd=/intel-ucode.img initrd=/initramfs-linux.img' --verbose`
# efibootmgr -v` to list boot entry then choose boot entry by run:
`$ efibootmgr --bootorder XXXXX --verbose` where XXXXX is a numbre of boot entry 
`# exit` then `$ umount -a`
`# reboot`
  ######Select best mirrors:#############
connect to internet with `# nmcli or nmtui`
`# cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.back` as root, to backup.
`# reflector --verbose --latest 5 --sort rate --save /etc/pacman.d/mirrorlist`.
`# pacman -Syu`.
  ######Now install Needed futures:######
`# sudo pacman -S mesa vulkan-intel xorg bash-completion alsa-utils alsa-plugins pulseaudio pulseaudio-equalizer pulseaudio-alsa pulseaudio-bluetooth zsh zsh-completions` then reboot.
`# sudo pacman -S gnome gnome-extra` if you wanna use gnome DE.
`# sudo systemctl enable gdm.service`
  #####Enable keyboard layout:###########
`# sudo vim /etc/X11/xorg.conf.d/00-keyboard.conf` then add:
 ##################################################
 # Section "InputClass"
 #       Identifier "system-keyboard"
 #       MatchIsKeyboard "on"
 #       Option "XkbLayout" "us,ara"
 #       Option "XkbModel" "pc104"
 #       Option "XkbOptions" "grp:alt_shift_toggle"
 # EndSection
 ##################################################
