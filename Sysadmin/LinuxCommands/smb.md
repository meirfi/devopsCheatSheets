# SMB & NFS Mounts

## Mount Samba share on Ubuntu
```bash
sudo apt-get install cifs-utils
```

```bash
check SMB Connection
smbclient -L <DOAMIN_SERVER> -U <USER_NAME> -W <DOAMIN_NAME>

mount -t cifs <DOMAIN_SHARE> <MOUNT_DIRECTORY> --verbose -o rw,noserverino,noexec,nodev,nosuid,uid=race,gid=900,file_mode=0664,dir_mode=0775,nocase,iocharset=utf8,soft,user=<USER_NAME>,domain=<DOMAIN_NAME>

mount --verbose -t cifs  //wnasfs/rtcpublic /tmp/builds/ -o username=svcrtca -vvv


or adding 

credentials=/root/cifs.creds
# instead of user/domain/pass

username=<USER_NAME>
password=<PASSWORD>
domain=<DOMAIN_NAME>
```