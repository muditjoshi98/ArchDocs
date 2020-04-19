# Arch Install Dual-Boot

### Installation is done in UEFI mode.

Here we are installing Arch Linux alongside Windows 10, which was already installed.

Installation steps might change from time to time but basic steps always remains same. Refer to [Arch Wiki](https://wiki.archlinux.org/) for latest steps.

1. Connect to a network
    1. `dhcpcd` if wired nework is not working.
    
    2. `wifi-menu` for connecting via wireles-network, also metion interface.
    3. Check your connection `ping -c3 google.com`, if you are receiving packages you are good to go.
    
2. Check for drive type and storage using `# fdisk -l`

3. A clean Arch install requires 3 patitions namely **EFI Partition**, **swap** and **root `/`**. User can also have a separate **`/home`** partition if needed.

4. IN this case we don't need EFI partiton we will be using already existing partion created by Windows 10 and swap partition is not necessary nowadays in place of this people generally use swap file.

5. Create Partitons : `cfdisk` utility is used to create partitions. Select `gpt` for UEFI/GPT mode(used here) and `dos` for UEFI/MBR mode.
    1.  Partitoning EFI system (If required): 
        * `New`
        * `500M` (recommended)
        * `Type`
        * `EFI System`
    2. Partitoning Linux File System : 
        * `New`
        * `30G`
    3.  ~~Partitoning Swap : (Old method for swap-do not use)~~
        * ~~`New`~~
        * ~~`Recommended size - Double the memory of RAM`~~
        * ~~`Type`~~
        * ~~`Linux Swap`~~
    4. Home Patition (Optional) :
        * `New`
        * `Remaining partition size`
        * `Type`
        * `Linux Home` 
    5. `Write`, then type *"yes"* and press Enter.
    6. `Quit`

6. Format the partitons and change their file type respectively.
    * ~~`# mkfs.fat -F32 /dev/sda1` (EFI partiton)~~ **Remember not to format EFI partition here other we cannot boot into Windows also this is only done for clean install.**
    * `# mkfs.ext4 /dev/sda2` (Linux File System Partition)
    * `# mkfs.ext4 /dev/sda3` (Linux Home Partition)
    * ~~`# mkswap /dev/sda4` (Swap Partiton)~~
    * ~~`# swapon /dev/sda4` (start using swap)~~

    There the partiton name can be different run `fdisk -l` to see partitions in your system.

7. Mount You file systems :
    * Linux File System : `# mount /dev/sda2 /mnt`.
    * `# mkdir /mnt/home`
    * Linux Home Partition : `# mount /dev/sda3 /mnt/home`.
    * `# mkdir /mnt/boot/efi`
    * Linux EFI Partition : `# mound /dev/sda1 /mnt/boot/efi`.
    
    Dont forget to create respective directories if they are not present

8. Chek whether they are mounted properly using `lsbk -l`

9. Install Arch linux package: `# pacstrap /mnt base base-devel linux linux-firmware sudo vim nvim`.

10. Generate fstab file: `# genfstab -U -p /mnt >> /mnt/etc/fstab`.

11. Go to arch-linux installation root: `# arch-chroot /mnt`.

11. Install some other softwares: `# pacaman -S grub efibootmgr dosfstools os-prober mtools linux-headers network-manager`.

12. Set your locale: `# nano /etc/locale.gen` (uncomment your locale lines).

13. Generate locale `# locale-gen` and `# echo "Your loacle" > /etc/locale.conf`.

14. Set the time
    * `# ln -sf /usr/share/zoneinfo/<path_to_your_timezone> /etc/localtime`
    * `# hwclock --systohc --utc`
    * Check date using `timedatectl`

15. Set hostname
    * `echo <pc_name> > /etc/hostname`
    * open `/etc/hosts` files and add below lines then save and exit.
    ```
        127.0.0.1   localhost
        ::1     localhost
        127.0.1.1   <pc_name>.localdomain <pc_name>
      ```

16. Enable System Manager to connect to internet next time you run arch `# systemctl enable NetworkManager`

17. Set root password: `# passwd` then enter password 2 times.

18. Install grub bootloader: `# grub-install --target=x86_64-efi --bootloader-id=grub --recheck`.
    
    Refer to [Archwiki-GRUB](https://wiki.archlinux.org/index.php/GRUB)

19. Copy locale to grub: `# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo`.

20. Gen grub conf file: `# grub-mkconfig -o /boot/grub/grub.cfg`

21. Creating swap file: (new way, use this method if you want to use swap)
    * `# fallocate -l 2G /swapfile`, here 2G is file size i.e. 2GB
    * `# chmod 600 /swapfile`
    * `# mkswap /swapfile`
    * `# swapon /swapfile`
    * `# echo '/swapfile none swap sw 0 0' | tee -a /etc/fstab`
    * Check whether your swap is working using command `free -m`

22. Come out of chroot: `# exit`

23. Unmount all drives: `# umount -a`

24. Restart you system and login as root.

25. Add a user to your system
    * `useradd -m -g users -G wheel -s /bin/bash <user_name>`
    * change password using `passwd`
    * Allow sudo previlidges to your user 
        * run `visudo`
        * Uncomment `%wheel ALL=(ALL) ALL` by removing `#`
        * Save and exit.

26. Install display server and audio drivers `pacman -S pulseaudio pulseaudio-alsa xorg xorg-xinit xorg-server xorg-server-common xf86-input-libinput xorg-xset`

27. Now basic installation is complete, from it depends on you how you proceed further. Refer to [General Recommendations](https://wiki.archlinux.org/index.php/General_recommendations) and [List of Applications](https://wiki.archlinux.org/index.php/List_of_applications)

