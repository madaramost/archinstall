###### General Installation procedure (standard install on EFI):
  01. `# cfdisk /dev/sda` then make partitions. 
  02. `# mkfs.fat -F32 /dev/sda1` Skip if already had EFI partition.
  03. `# mkswap /dev/sda4` then `swapon /dev/sda4`
  04. `# mkfs.ext4 /dev/sda5`
  05. `# mkfs.ext4 /dev/sda6`
  06. `# mount /dev/sda6 /mnt`
  07. `# mkdir /mnt/home`
  08. `# mount /dev/sda5 /mnt/home`
  09. `# mkdir /mnt/boot`
  10. `# mount /dev/sda1 /mnt/boot`
  11. `# pacstrap -i /mnt base base-devel`
  12. `# genfstab -U -p /mnt >> /mnt/etc/fstab`
  13. `# arch-chroot /mnt`
  14. `# passwd root`
  15. `# useradd -m -g users -G wheel,storage,power -s /bin/bash sentaku` then passwd sentaku
  16. `# EDITOR=nano visudo`. and uncomment : %wheel ALL=(ALL) ALL
  17. `# nano /etc/locale.gen` (uncomment en_US.UTF-8)
  18. `# locale-gen`
  19. `# echo LANG=en_US.UTF-8 > /etc/locale.conf`
  20. `# export LANG=en_US.UTF-8`
  21. `# ln –s /usr/share/zoneinfo/Africa/Algiers /etc/localtime`
  22. `# hwclock --systohc --utc`
  23. `# echo X1C-Pro > /etc/hostname`
  24. `# mkinitcpio –p linux`
  #######for grub ######################
  25. `# pacman -S grub efibootmgr dosfstools os-prober mtools linux-headers dialog wpa_supplicant`
  26. `# mkdir /boot/EFI`
  27. `# mount /dev/sda1 /boot/EFI`
  28. `# grub-install --target=x86_64-efi  --bootloader-id=grub_uefi --recheck`
  29. `# grub-mkconfig -o /boot/grub/grub.cfg`
  30. `# grub-install --target=x86_64-efi  --bootloader-id=grub_uefi --recheck`
  31. `# grub-mkconfig -o /boot/grub/grub.cfg`
  ######for bootctl ###################
  25. `# pacman -S fuse bash-completion intel-ucode ntfs-3g os-prober linux-headers dialog wpa_supplicant`
  26. `# bootctl --path=/boot install`
  27. `# nano /boot/loader/entries/arch.conf` and edit it:
  #################################
  title   Arch Linux              #
  linux   /vmlinuz-linux          #
  initrd  /intel-ucode.img        #
  initrd  /initramfs-linux.img    #
  options root=UUID=.... rw       #
  #################################
  28. `$ exit`
  29. `# umount -a` /* not needed for bootctl*/
  30. `# reboot`
  ######Select best mirrors:#############
  1.  `# cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.back` as root, to backup.
  2.  `# reflector --verbose --latest 5 --sort rate --save /etc/pacman.d/mirrorlist`.
  3.  `# pacman -Syu` .
  ######Now install Needed futures:######
  01. `# sudo pacman -S bash-completion xorg alsa-utils pulseaudio zsh` then reboot.
  02. `# sudo pacman -S gnome gnome-extra` if you wanna use gnome DE.
  03. `# sudo systemctl enable NetworkManager.service`
  04. `# sudo systemctl enable gdm.service`
