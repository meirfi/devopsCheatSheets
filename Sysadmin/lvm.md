# Logical Volume Manager (LVM)
## what is LVM 

- pv: physical device (e.g. /dev/md0 or /dev/sda1)
- vg: volume group (consists of 1 or more pvs, contains lvs); has a name (e.g. lvm)
- lv: logical volume (has a name which defines its path, e.g. /dev/lvm/root which equals dev/mapper/lvm-root)

Listing Items
- ```sudo pvdisplay``` - List physical devices.
- ```sudo vgdisplay``` - List volume groups.
- ```sudo lvdisplay``` - List logical volumes.

### Create Physical Volume
Create a physical volume on a drive. This is required before you can add it to a volume group or create a volume group from it.
```bash
pvcreate /dev/sd[x]
```
command exmple :
```bash
pvcreate /dev/sdb /dev/sdc
```
### Create Volume Group
Volume groups are collections of physical volumes. To create one, you need to specify which volumes it should group/manage.

```bash
vgcreate [new volume group name] /dev/sd[x] /dev/sd[x]
```

### Create Logical Volume
Create an LVM by adding it to a Volume Group that already exists.
```bash
lvcreate -L [Size in GB]G [Volume Group Name]
```
or to create just use the entire space:

```bash 
lvcreate -l 100%FREE [Volume Group Name] 
```
Command Example:

``bash
$ lvcreate -l 100%FREE testvg
``

| command | description |
|---------|-------------|
| `pvcreate /dev/md0` | initializes `/dev/md0` as phys device for a volume group
| `vgcreate lvm /dev/md0` | create volume group `lvm` with phys device `/dev/md0`
| `lvcreate -L30G -nroot lvm ; mkfs.ext4 /dev/lvm/root` | create logical volume `root`, sized 30G in volume group `lvm`; format with ext4
| `lvextend -L60G -nroot lvm ; resize2fs /dev/lvm/root` | extend `/dev/lvm/root` to 60G; also resize file system to new size
| `pvs`, `vgs`, `lvs` | show short info about pv, vg and lv
| `pvdisplay`, `vgdisplay`, `lvdisplay` | show long info
| `pvscan /dev/md0` | scan disks for physical volumes (e.g. when running live system)
| `vgextend lvm /dev/md1` | add phys device `/dev/md1` to volume group `lvm` (need pvcreate first!)
| `pvmove /dev/md0 ; vgreduce lvm /dev/md0` | move all logical volumes from `/dev/md0` and remove phys device from volume group
