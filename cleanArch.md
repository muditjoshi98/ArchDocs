# Clean Arch

## 1. Clean Packages Cache
* Check size the cache package takes : `du -sh /var/cache/pacman/pkg/`
* Remove currently uninstalled cache packages : `sudo pacman -Sc`
* Remove all old packages : `sudo pacman -Scc`
* To get any of those old packages : [ArchLinux Achive](https://wiki.archlinux.org/index.php/Arch_Linux_Archive)

### Automatic Way : 
* Install Paccache : `sudo pacman -S pacman-contrib`
* Dryrun : `paccache -d`
* Remove : `paccache -r`

## 2. Remove Orphan Packages
* List packages : `pacman -Qtdq`
* Remove packages : `sudo pacman -R $(pacman -Qtdq)`

## 3. Remove Cache from Home
* Check size : `du -sh ~/.cache`
* Remove files : `rm -rf ~/.cache/*`

## 4. Other
* Remove old config files.
* Remove duplicate or unnecessary files using `rmlint`
* Check for large files using `KDE-filelight` or `Gnome-baobab`

## OR you can use a Disk Cleanup Program

# Formatting USB
1. `sudo fdisk -l`
2. `sudo umount /dev/* `
3. Choose respective option :-
    * For FAT : `sudo mkfs.vfat -n *device name* -I /dev/*`
    * For NTFS : `sudo mkfs.ntfs -I /dev/*`
    * For ext4 : `sudo mkfs.ext4 -n  -I /dev/*`
4. We can also use following commands to completely wipe out the whole USB flash drive
    * `sudo shred /dev/*`
    * `sudo dd if=/dev/zero of=/dev/*`

## More details at `man mkfs`

#