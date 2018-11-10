# linux/unix xargs 
## what is xargs

xargs command in unix or Linux is a powerful command used in conjunction with **find** and **grep** command in linux to divide a big list of arguments into small list received from standard input.<br>find and grep command produce long list of file names and we often want to either remove them or do some operation on them but many unix operating system doesn't accept such a long list of argument.<br>UNIX xargs command divide that list into sub-list with acceptable length and made it work.<br> This Unix tutorial is in continuation of my earlier post on Unix like 10 examples of chmod command in Unix and How to update soft link in Linux.<br>If you haven’t read those unit tutorial than check them out.<br> By the way In this tutorial we will see different example of unix xargs command to learn how to use xargs command with find and grep and other unix command and make most of it. Though what you can do with xargs in unix can also be done by using options provided in find but believe xargs is much easy and powerful.

## xargs command examples
###  Xargs with and without xargs
```bash 
testuser@test:/etc find . -name "*bash*"
./bash.bashrc
./bash.bash_logout
./defaults/etc/bash.bashrc
./defaults/etc/bash.bash_logout
./defaults/etc/skel/.bashrc
./defaults/etc/skel/.bash_profile
./postinstall/bash.sh.done
./setup/bash.lst.gz
./skel/.bashrc
./skel/.bash_profile

testuser@test:/etc find . -name "*bash*" | xargs
./bash.bashrc ./bash.bash_logout ./defaults/etc/bash.bashrc ./defaults/etc/bash.bash_logout ./defaults/etc/skel/.bashrc ./defaults/etc/skel/.bash_profile ./postinstall/bash.sh.done ./setup/bash.lst.gz ./skel/.bashrc ./skel/.bash_profile

``` 
### xargs and grep
```bash 
find . -name "*.java" | xargs grep "Stock"
```