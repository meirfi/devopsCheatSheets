# How to fix "error: unknown filesystem. grub rescue> 

First boot into Ubuntu from an ISO image.

Locate the Ubuntu partition and the folder containing the GRUB modules.

The GRUB folder containing the modules must be located so the correct modules can be loaded. This folder would have been created during the initial installation of Ubuntu and should be located in the Ubuntu partition. This folder would normally be located at either (hdX,Y)/boot/grub or (hdX,Y)/usr/lib/grub/i386-pc. Find your existing Ubuntu partition and the module folder.

```bash
ls                               # List the known drives (hdX) and partitions (hdX,Y)
ls (hdX,Y)/                      # List the contents of the partition's root
ls (hdX,Y)/boot/grub             # Normal location of the Grub 2 modules.
ls (hdX,Y)/usr/lib/grub/i386-pc  # Alternate location of the Grub 2 modules.
ls - should return all known drives (hdX) and partitions (hdX,Y)
ls (hdX,Y)/ - should show the contents of the root directory of the partition.
```
If you get an "error: unknown filesystem" this is not your Ubuntu partition.
If this is the Ubuntu partition, you will see the Ubuntu folders, including lost+found/, home/, boot/ and vmlinuz and initrd.img. Use this address as the first part of the next command.
```bash
ls (hdX,Y)/boot/grub - should display several dozen *.mod files. This is the folder you are looking for.
```
If you don't find the modules, try the alternate location: ls (hdX,Y)/usr/lib/grub/i386-pc
Load the modules.
```bash
set prefix=(hdX,Y)/<path to modules>
```
This command must correctly point to the folder containing the GRUB modules. The address should be the one in the previous section which displayed the modules.
Examples:
```bash
set prefix=(hd0,5)/boot/grub 
set prefix=(hd1,1)/usr/lib/grub/i386-pc
Load modules:

insmod linux
insmod loopback
insmod iso9660
insmod fat        # If ISO is located on fat16 or fat32 formatted partition.
insmod ntfs       # If ISO is located on an NTFS formatted partition.
insmod nftscomp   # If NTFS compression is used on the partition. Load if you aren't sure.
```
A "file not found" error means that the path in the prefix is incorrect or the specific module does not exist. The prefix setting may be reviewed with the set command. Rerun the "set prefix=" command with the proper path.

Locate the Ubuntu ISO file.

Using the combinations of ls commands, locate the Ubuntu ISO image.
Create the loopback device.

loopback loop (hdX,Y)/<path to ISO>/<ISO-name.iso>
Example:
```bash
loopback loop (hd1,1)/path/to/ubuntu-10.04.1-desktop-i386.iso
```
Load the Linux kernel and initrd image.
```bash
set root=(loop)
linux /casper/vmlinuz boot=casper iso-scan/filename=/<ISO-name.iso> noprompt noeject
initrd /casper/initrd.lz
```
If the path to the ISO or filename is not correct, the boot will halt at the BusyBox screen and produce a message stating "can't open /dev/sr0: No medium found".
Note: If the ISO file is not in the / folder, include the path in the iso-scan/filename= entry. See second example.
Examples:
```bash
linux /casper/vmlinuz boot=casper iso-scan/filename=/ubuntu-10.04.1-desktop-i386.iso
linux /casper/vmlinuz boot=casper iso-scan/filename=/my-iso/ubuntu-10.04.1-desktop-i386.iso
```
Boot.

That should be it. If the commands ran without any messages/errors, the commands were accepted as entered. It's now time to boot:

boot
Further information is in forum post HOWTO: Boot & Install Ubuntu from the Grub Rescue Prompt

Now do this after booting:

How to fix: error:unknown file system grub rescue? is post with the same problem and is solved as below,
```bash
sudo mount /dev/sdaX /mnt
```
Here, sdaX is your boot partition. You can get a list with sudo blkid like this,
```bash
/dev/sda1: LABEL="Windows XP" UUID="96A4390DA438F0FB" TYPE="ntfs" 
/dev/sda3: LABEL="Ubuntu 11.04" UUID="b61fcae3-7744-45b4-95b9-7528d50a3652" TYPE="ext4" 
/dev/sda5: LABEL="Se7en" UUID="A2DC9D71DC9D4109" TYPE="ntfs" 
/dev/sda6: LABEL="Development" UUID="DEB455A1B4557CC9" TYPE="ntfs" 
/dev/sda7: LABEL="EXTRA" UUID="D8A04109A040F014" TYPE="ntfs" 
/dev/sda8: LABEL="SONG" UUID="46080FCD080FBAC7" TYPE="ntfs" 
/dev/sda9: LABEL="BACKUPS" UUID="766E-BC99" TYPE="vfat" 
# Note: sdaX must be Linux partition.

sudo grub-install --boot-directory=/mnt/boot /dev/sda

sudo update-grub
```