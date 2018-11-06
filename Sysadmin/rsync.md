# rsync command


## how to copy entire linux root filesystem to new hard drive on with ssh and tar
### Use rsync. From the new host, you can use
- rsync -avP --numeric-ids --exclude='/dev' --exclude='/proc' --exclude='/sys' root@failedharddrivehost:/ /path/to/destination/
- rsync -avzp --exclude='/mnt' --exclude='/diskNew' --exclude='/proc' --exclude='/dev' --exclude='/sys' 9.151.213.240:/

## If both computers are on the same (safe) LAN
root@good_host$ cd good_partition; netcat -l -p 1234 | tar xvpmf -
root@bad_host$ tar -cv -f- --exclude=/proc --exclude=/sys / | netcat good_host.ip 1234

However, you should (also) consider to make a dd dump of the failing drive's partitions:

user@good_host$ cd good_partition; netcat -l -p 1234 > dump_of_bad_partition_1.dd
root@bad_host$ dd if=/dev/sda1 | netcat good_host.ip 1234

### If you do then boot from a live CD. Then use:

- dump (dump/restores whole filesystems including its permissions).
- Tar with /dev excluded. You can combine this with outputting to std_out and piping that though netcat
### The exclude syntax is: tar --exclude='/dev'.
- or rsync with the same excludes. E.g.
```rsync -zvr --exclude /dev/ / destination_computer_name_or_ip```
- or use dd like this: 
nc -l 4242 | gunzip | cat > my_full_disk_backup_of_PC_named_foo 
dd if=/dev/sda of=- bs=1M | gzip | nc -p 4242 name_of_the_destination