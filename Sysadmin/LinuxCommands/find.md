# find commnad


## finding number of Inodes on the system

```bash
echo "Inode usage for: $(pwd)" ; for d in `find -maxdepth 1 -type d |cut -d\/ -f2 |grep -xv . |sort`; do c=$(find $d |wc -l) ; printf "$c\t\t- $d\n" ; done ; printf "Total: \t\t$(find $(pwd) | wc -l)\n"
Inode usage for: /home/theuser
26              - attachments
2               - .cpaddons
64              - .cpanel
1               - downloads
20              - etc
1               - .htpasswds
2               - .HttpRequest
25084           - mail
2               - .matplotlib
9               - .MirrorSearch
1               - perl5
6               - public_ftp
7466            - public_html
4               - .softaculous
1               - .sqmailattach
2               - .sqmaildata
11              - ssl
959             - templates_c
682             - tmp
1               - .trash
Total:          34379
```