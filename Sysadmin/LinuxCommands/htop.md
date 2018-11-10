# htop - Linux Process Monitoring

[htop-process]: images/htop/htop-processes-monitoring.png "htop-process-list"
[htop-setup]: images/htop/htop-setup-screen.png "htop-setup"
[htop-tree]: images/htop/htop-process-view-in-tree-format.png "htop-tree"


[htop-small]: images/htop/htop-small.png "small"
[htop-top]: images/htop/htop-top.png "top"
[htop-bottom]: images/htop/htop-bottom.png "bottom"

htop is an interactive process monitor. It’s one of my favorite linux tools that I use regularly to monitor system resources. If you take top and put it on steroids, you get htop.

## Tag
hastag Tools and Monitoring Linux Performance

## How to install htop command

- RHEL/CentOS Installation via EPEL Repo
    - On RHEL/CentOS – 32-bit OS
    ```bash
    -------------- For RHEL/CentOS 6 --------------
    $ wget http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
    $ rpm -ihv epel-release-6-8.noarch.rpm
    ```
    - On RHEL/CentOS – 64-bit OS
    ```bash
    -------------- For RHEL/CentOS 7 --------------
    $ wget dl.fedoraproject.org/pub/epel/7/x86_64/Packages/e/epel-release-7-11.noarch.rpm
    $ rpm -ihv epel-release-7-11.noarch.rpm 

    -------------- For RHEL/CentOS 6 --------------
    $ wget http://download.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
    $ rpm -ihv epel-release-6-8.noarch.rpm
    ```
    - intallting the package
    ```bash
    $ yum install htop
    # or
    $ dnf install htop      [On Fedora 22+ releases]
    ```
- Debian and Ubuntu Installation
  ```bash
  $ sudo apt-get install htop
  ```
### Compile and Install Htop from Source Packages
- RHEL/CentOS and Fedora
  ```bash
  $ yum groupinstall "Development Tools"
  $ yum install ncurses ncurses-devel
  $ wget http://hisham.hm/htop/releases/2.0.2/htop-2.0.2.tar.gz
  $ tar xvfvz htop-2.0.2.tar.gz
  $ cd htop-2.0.2
  ```
- Debian and Ubuntu
  ```bash
  $ sudo apt-get install build-essential  
  $ sudo apt-get install libncurses5-dev libncursesw5-dev
  $ wget http://hisham.hm/htop/releases/2.0.2/htop-2.0.2.tar.gz
  $ tar xvfvz htop-2.0.2.tar.gz
  $ cd htop-2.0.2
  ```
- configure and make
  ```bash
  $ ./configure
  $ make
  $ make install
  ```

## How to use htop?
Now run the htop monitoring tool by executing following command on the terminal.

### Htop is having three sections mainly
- Header, where we can see info like **CPU**, Memory, Swap and also shows tasks, **load average** and **Up-time**.
- List of processes sorted by **CPU** utilization.
- Footer shows different options like **help**, **setup**, **filter tree kill**, **nice** , **quit** etc.
![htop-process][htop-process]


Press **F2** or **S** for setup menu > there are four columns i.e **Setup, Left Column, Right Column** and **Available Meters**.
![htop-setup][htop-setup]
Type **tree** or **t** to display processes tree view.

![htop-tree][htop-tree]

## Htop Shortcut and Function Keys

| description        | Function Keys           | Shortcut keys  |
| ------------- |:-------------:|:-----:|
| help                     | F1  | h |
| setup                    | F2  | s |
| Search Process           | F3  | / |
| Invert Sort Order        | F4  | | |
| Tree                     | F5  | t |
| Sort By                  | F6  | > |
| Nice - (Change Priority) | F7  | [ |
| Nice + (Change Priority) | F8  | ] |
| Kill a Process           | F9  | k |
| Quite                    | F10 | q |

## htop Explained Visually

Here’s what htop looks like when you first run it.

![htop-small][htop-small]

I’ve separated the interface into upper and lower sections so I have enough room to annotate.

Let’s start with the upper section.

![htop-small][htop-top]

Here’s the lower section of htop.

![htop-small][htop-bottom]