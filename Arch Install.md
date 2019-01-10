###### General Installation procedure (standard install on EFI):
  01. `# cfdisk /dev/sda` then make partitions. 
  02. `# mkfs.fat -F32 /dev/sda1` Skip if already had EFI partition.
  03. `# mkswap /dev/sda4`
  04. `# mkfs.ext4 /dev/sda5`
  05. `# mkfs.ext4 /dev/sda6`
  06. `# mount /dev/sda6 /mnt`
  07. `# mkdir /mnt/home`
  08. `# mount /dev/sda5 /mnt/home`
  09. `# pacstrap -i /mnt base base-devel`
  10. `# genfstab -U -p /mnt >> /mnt/etc/fstab`
  11. `# arch-chroot /mnt`
  12. `# passwd root`
  13. `# useradd -m -g users -G wheel,storage,power -s /bin/bash sentaku` 
  14. `# EDITOR=nano visudo`. and uncomment : %wheel ALL=(ALL) ALL
  15. `# nano /etc/locale.gen` (uncomment en_US.UTF-8)
  16. `# locale-gen`
  17. `# echo LANG=en_US.UTF-8 > /etc/locale.conf`
  18. `# export LANG=en_US.UTF-8`
  19. `# ln –s /usr/share/zoneinfo/Africa/Algiers /etc/localtime`
  20. `# hwclock --systohc --utc`
  21. `# echo X1C-Pro > /etc/hostname`
  22. `# mkinitcpio –p linux`
  23. `# pacman -S grub efibootmgr dosfstools os-prober mtools linux-headers`
  24. `# mkdir /boot/EFI`
  25. `# mount /dev/sda1 /boot/EFI`
  26. `# grub-install --target=x86_64-efi  --bootloader-id=grub_uefi --recheck`
  27. `# grub-mkconfig -o /boot/grub/grub.cfg`
  29. `$ exit`
  30. `# umount -a`
  31. `# reboot`
Now install Needed futures:
  01. `# sudo pacman -S bash-completion xorg alsa-utils pulseaudio zsh` then reboot.
  02. `# sudo pacman -S gnome gnome-extra` if you wanna use gnome DE.
  03. `# sudo systemctl enable NetworkManager.service`
  04. `# sudo systemctl enable gdm.service`
