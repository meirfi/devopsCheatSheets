# How to Repair, Restore, or Reinstall Grub 2 with a Ubuntu Live CD or USB
Grub 2 typically gets overridden when you install Windows or another Operating System.<br>
To make Ubuntu control the boot process, you need Reinstall (Repair/Restore) Grub using a Ubuntu Live CD.

## Repare Grub 2 Steps 

- Boot with LiveCD or any other Linux Distro, prefered Ubuntu
- Open Terminal Command Line
- Mount the partition your Ubuntu or any disto you have Installed.<br>It is usually a EXT4 Partition.<br>Replace the XY with the drive letter, and partition number, for example: sudo mount /dev/sda1 /mnt.<br>
``bash
$ sudo mount /dev/sda1 /mnt
``
- Now bind the directories that grub needs access to to detect other operating systems, like so. 
    ```bash
    sudo mount --bind /dev /mnt/dev &&
    sudo mount --bind /dev/pts /mnt/dev/pts &&
    sudo mount --bind /proc /mnt/proc &&
    sudo mount --bind /sys /mnt/sys
    ```

- Now we jump into the file system by using chroot command
    ```bash
    sudo chroot /mnt
    ```

- Now install, check, and update grub.<br>
This time you only need to add the drive letter (usually a) to replace X, for example: grub-install /dev/sda, grub-install –recheck /dev/sda.

```bash
$ grub-install /dev/sdX
$ grub-install --recheck /dev/sdX
$ update-grub
```

- Now grub is back, all that is left is to exit the chrooted system and unmount everything.

```bash
exit &&
sudo umount /mnt/sys &&
sudo umount /mnt/proc &&
sudo umount /mnt/dev/pts &&
sudo umount /mnt/dev &&
sudo umount /mnt
```
- Shut down and turn your computer back on, and you will be met with the default Grub2 screen.<br>
You may want to update grub or re-install burg however you like it.