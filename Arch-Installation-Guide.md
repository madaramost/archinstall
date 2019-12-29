 ###### General Installation procedure (standard install on EFI) in "01/01/2020":<br/>
`# cfdisk /dev/sda` then make partitions.<br/>
`# mkfs.fat -F32 /dev/sda1` Skip if already had EFI partition.<br/>
`# mkswap /dev/sda4` then `swapon /dev/sda4`<br/>
`# mkfs.ext4 /dev/sda5`<br/>
`# mkfs.ext4 /dev/sda6`<br/>
`# mount /dev/sda6 /mnt`<br/>
`# mkdir /mnt/home`<br/>
`# mount /dev/sda5 /mnt/home`<br/>
`# mkdir /mnt/boot`<br/>
`# mount /dev/sda1 /mnt/boot`<br/>
`# pacstrap /mnt base base-devel linux linux-firmware linux-headers`<br/>
`# genfstab -U /mnt >> /mnt/etc/fstab`<br/>
`# arch-chroot /mnt`<br/>
`# passwd` root passwd<br/>
`# pacman -S vim networkmanager` then enable NetworkManager.service<br/>
`# useradd -m -g users -G wheel,storage,power,video,audio -s /bin/bash sentaku` then `# passwd sentaku`<br/>
`# EDITOR=vim visudo`. and uncomment : %wheel ALL=(ALL) ALL<br/>
`# vim /etc/locale.gen` (uncomment en_US.UTF-8)<br/>
`# locale-gen`<br/>
`# echo LANG=en_US.UTF-8 > /etc/locale.conf`<br/>
`# export LANG=en_US.UTF-8`<br/>
`# ln -sf /usr/share/zoneinfo/Africa/Algiers /etc/localtime`<br/>
`# hwclock --systohc`<br/>
`# echo X1C-Pro > /etc/hostname`<br/>
`# mkinitcpio -P`<br/>
  ######Instaling EFISTUB boot loader #####<br/>
`# pacman -S fuse intel-ucode ntfs-3g efibootmgr`<br/>
`# efibootmgr --disk /dev/sda1 --part 1 --create --label "Arch Linux" --loader /vmlinuz-linux --unicode 'root=PARTUUID=ForRoot quiet loglevel=3 rd.systemd.show_status=auto rd.udev.log_priority=3 rw resume=PARTUUID=ForSwap initrd=/intel-ucode.img initrd=/initramfs-linux.img' --verbose`<br/>
`# efibootmgr -v` to list boot entry then choose boot entry by run:<br/>
`$ efibootmgr --bootorder XXXXX --verbose` where XXXXX is a numbre of boot entry<br/> 
`# exit` then `$ umount -a`<br/>
`# reboot`<br/>
  ######Select best mirrors:#############<br/>
connect to internet with `# nmcli or nmtui`<br/>
`# cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.back` as root, to backup.<br/>
`# reflector --verbose --latest 5 --sort rate --save /etc/pacman.d/mirrorlist`.<br/>
`# pacman -Syu`.<br/>
  ######Now install Needed futures:######<br/>
`# sudo pacman -S mesa vulkan-intel xorg bash-completion alsa-utils alsa-plugins pulseaudio pulseaudio-equalizer pulseaudio-alsa pulseaudio-bluetooth zsh zsh-completions` then reboot.<br/>
`# sudo pacman -S gnome gnome-extra` if you wanna use gnome DE.<br/>
`# sudo systemctl enable gdm.service`<br/>
  #####Enable keyboard layout:###########<br/>
`# sudo vim /etc/X11/xorg.conf.d/00-keyboard.conf` then add:<br/>
 ##################################################<br/>
 `# Section "InputClass"<br/>
        Identifier "system-keyboard"<br/>
        MatchIsKeyboard "on"<br/>
        Option "XkbLayout" "us,ara"<br/>
        Option "XkbModel" "pc104"<br/>
        Option "XkbOptions" "grp:alt_shift_toggle"<br/>
  EndSection<br/>`
 ##################################################
