#Netstat Commands for Linux Network Management

This tool is very important and much useful for Linux network administrators as well as system administrators to monitor and troubleshoot their network related problems and determine network traffic performance. This article shows usages of netstat command with their examples which may be useful in daily operation.

You might also be interested in following article


## Listing all the LISTENING Ports of TCP and UDP connections
Listing all ports (both **TCP** and **UDP**) using netstat `-a` option.
    
```bash 
 $ netstat -a | more
 Active Internet connections (servers and established)
 Proto Recv-Q Send-Q Local Address               Foreign Address             State
 tcp        0      0 *:sunrpc                    *:*                         LISTEN
 tcp        0     52 192.168.0.2:ssh             192.168.0.1:egs             ESTABLISHED
 tcp        1      0 192.168.0.2:59292           www.gov.com:http            CLOSE_WAIT
 tcp        0      0 localhost:smtp              *:*                         LISTEN
 tcp        0      0 *:59482                     *:*                         LISTEN
 udp        0      0 *:35036                     *:*
 udp        0      0 *:npmp-local                *:*
 Active UNIX domain sockets (servers and established)
 Proto RefCnt Flags       Type       State         I-Node Path
 unix  2      [ ACC ]     STREAM     LISTENING     16972  /tmp/orbit-root/linc-76b-0-6fa08790553d6
 unix  2      [ ACC ]     STREAM     LISTENING     17149  /tmp/orbit-root/linc-794-0-7058d584166d2
 unix  2      [ ACC ]     STREAM     LISTENING     17161  /tmp/orbit-root/linc-792-0-546fe905321cc
 unix  2      [ ACC ]     STREAM     LISTENING     15938  /tmp/orbit-root/linc-74b-0-415135cb6aeab
```
## Listing TCP Ports connections
Listing only **TCP** (Transmission Control Protocol) port connections using netstat ``-at``.

    ```bash
    $ netstat -at
    Active Internet connections (servers and established)
    Proto Recv-Q Send-Q Local Address               Foreign Address             State
    tcp        0      0 *:ssh                       *:*                         LISTEN
    tcp        0      0 localhost:ipp               *:*                         LISTEN
    tcp        0      0 localhost:smtp              *:*                         LISTEN
    tcp        0     52 192.168.0.2:ssh             192.168.0.1:egs             ESTABLISHED
    tcp        1      0 192.168.0.2:59292           www.gov.com:http            CLOSE_WAIT
    ```

## Listing UDP Ports connections
Listing only **UDP** (User Datagram Protocol ) port connections using netstat ``-au``.

    ```bash
    $ netstat -au
    Active Internet connections (servers and established)
    Proto Recv-Q Send-Q Local Address               Foreign Address             State
    udp        0      0 *:35036                     *:*
    udp        0      0 *:npmp-local                *:*
    udp        0      0 *:mdns                      *:*
    ```
## Listing all LISTENING Connections
Listing all active listening ports connections with netstat ``-l``.

    ```bash
    $ netstat -l
    Active Internet connections (only servers)
    Proto Recv-Q Send-Q Local Address               Foreign Address             State
    tcp        0      0 *:sunrpc                    *:*                         LISTEN
    tcp        0      0 *:58642                     *:*                         LISTEN
    tcp        0      0 *:ssh                       *:*                         LISTEN
    udp        0      0 *:35036                     *:*
    udp        0      0 *:npmp-local                *:*
    Active UNIX domain sockets (only servers)
    Proto RefCnt Flags       Type       State         I-Node Path
    unix  2      [ ACC ]     STREAM     LISTENING     16972  /tmp/orbit-root/linc-76b-0-6fa08790553d6
    unix  2      [ ACC ]     STREAM     LISTENING     17149  /tmp/orbit-root/linc-794-0-7058d584166d2
    unix  2      [ ACC ]     STREAM     LISTENING     17161  /tmp/orbit-root/linc-792-0-546fe905321cc
    unix  2      [ ACC ]     STREAM     LISTENING     15938  /tmp/orbit-root/linc-74b-0-415135cb6aeab
    ```

## Listing all TCP Listening Ports
Listing all active listening **TCP** ports by using option netstat ``-lt``.

    ```bash
    $ netstat -lt
    Active Internet connections (only servers)
    Proto Recv-Q Send-Q Local Address               Foreign Address             State
    tcp        0      0 *:dctp                      *:*                         LISTEN
    tcp        0      0 *:mysql                     *:*                         LISTEN
    tcp        0      0 *:sunrpc                    *:*                         LISTEN
    tcp        0      0 *:munin                     *:*                         LISTEN
    tcp        0      0 *:ftp                       *:*                         LISTEN
    tcp        0      0 localhost.localdomain:ipp   *:*                         LISTEN
    tcp        0      0 localhost.localdomain:smtp  *:*                         LISTEN
    tcp        0      0 *:http                      *:*                         LISTEN
    tcp        0      0 *:ssh                       *:*                         LISTEN
    tcp        0      0 *:https                     *:*                         LISTEN
    ```
## Listing all UDP Listening Ports
Listing all active listening **UDP** ports by using option netstat ``-lu``.
    
    ```bash
    $ netstat -lu
    Active Internet connections (only servers)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State
    udp        0      0 0.0.0.0:54035           0.0.0.0:*
    udp        0      0 localhost:897           0.0.0.0:*
    udp        0      0 0.0.0.0:917             0.0.0.0:*
    udp        0      0 0.0.0.0:35808           0.0.0.0:*
    udp        0      0 0.0.0.0:mdns            0.0.0.0:*
    udp        0      0 0.0.0.0:ndmp            0.0.0.0:*
    udp        0      0 0.0.0.0:55286           0.0.0.0:*
    udp        0      0 0.0.0.0:22537           0.0.0.0:*
    ...
    ```

## Listing all UNIX Listening Ports
Listing all active **UNIX** listening ports using netstat ``-lx``.

    ```bash
    $ netstat -lx
    Active UNIX domain sockets (only servers)
    Proto RefCnt Flags       Type       State         I-Node Path
    unix  2      [ ACC ]     STREAM     LISTENING     28346    @Symantec-SmcIPC
    unix  2      [ ACC ]     STREAM     LISTENING     28741    @/tmp/.ICE-unix/2205
    unix  2      [ ACC ]     STREAM     LISTENING     25202    @sym_config_ipc
    unix  2      [ ACC ]     STREAM     LISTENING     26069    @/tmp/dbus-JkWIu3oj
    unix  2      [ ACC ]     STREAM     LISTENING     27384    @/tmp/.X11-unix/X0
    unix  2      [ ACC ]     STREAM     LISTENING     29526    @/tmp/dbus-PgwoAApT
    unix  2      [ ACC ]     STREAM     LISTENING     22125    /var/lib/mysql/mysql.sock
    unix  2      [ ACC ]     STREAM     LISTENING     28742    /tmp/.ICE-unix/2205
    unix  2      [ ACC ]     STREAM     LISTENING     13170    @ISCSID_UIP_ABSTRACT_NAMESPACE
    unix  2      [ ACC ]     STREAM     LISTENING     24653    /var/run/libvirt/libvirt-sock
    unix  2      [ ACC ]     STREAM     LISTENING     18582    /opt/cisco/hostscan/.ciscod.ipc
    ...
    ```

## Showing Statistics by Protocol
Displays statistics by protocol. By default, statistics are shown for the **TCP**, **UDP**, **ICMP**, and **IP protocols**. The -s parameter can be used to specify a set of protocols.

- Show Statistics 

    ```
    Ip:
        7727806 total packets received
        0 forwarded
        0 incoming packets discarded
        7702220 incoming packets delivered
        5992856 requests sent out
        88 dropped because of missing route
    Icmp:
        2383 ICMP messages received
        0 input ICMP message failed.
        ICMP input histogram:
            destination unreachable: 2
            timeout in transit: 2175
            echo requests: 6
            echo replies: 200
        2889 ICMP messages sent
        0 ICMP messages failed
        ICMP output histogram:
            destination unreachable: 159
            echo request: 3
            echo replies: 6
    IcmpMsg:
            InType0: 200
            InType3: 2
            InType8: 6
            InType11: 2175
            OutType0: 6
            OutType3: 159
            OutType8: 3
            OutType69: 2721
    Tcp:
        1095 active connections openings
        83 passive connection openings
        581 failed connection attempts
        66 connection resets received
        13 connections established
        7443005 segments received
        6047166 segments send out
        3737 segments retransmited
        3 bad segments received.
        193 resets sent
    Udp:
        65103 packets received
        2 packets to unknown port received.
        0 packet receive errors
        15209 packets sent
        0 receive buffer errors
        0 send buffer errors
    ```
- Statistics by TCP Protocol

    ```
    $ netstat -st
    IcmpMsg:
        InType0: 200
        InType3: 2
        InType8: 6
        InType11: 2175
        OutType0: 6
        OutType3: 159
        OutType8: 3
        OutType69: 2721
    Tcp:
        1095 active connections openings
        83 passive connection openings
        581 failed connection attempts
        66 connection resets received
        13 connections established
        7434153 segments received
        6041921 segments send out
        3737 segments retransmited
        3 bad segments received.
        193 resets sent
    ```

- Statistics by UDP Protocol
    ```
    $ netstat -su
    IcmpMsg:
        InType0: 200
        InType3: 2
        InType8: 6
        InType11: 2175
        OutType0: 6
        OutType3: 159
        OutType8: 3
        OutType69: 2721
    Udp:
        65054 packets received
        2 packets to unknown port received.
        0 packet receive errors
        15198 packets sent
        0 receive buffer errors
        0 send buffer errors
    UdpLite:
    IpExt:
        InNoRoutes: 1
        InMcastPkts: 55084
        OutMcastPkts: 5231
        InBcastPkts: 216953
        InOctets: 7249113262
        OutOctets: 2200297334
        InMcastOctets: 50124418
        OutMcastOctets: 5083030
        InBcastOctets: 43544824
        InNoECTPkts: 8661365
    ```
##   Displaying Service name with PID
Displaying service name with their **PID** number, using option ``netstat -tp`` will display **"PID/Program Name"**.

    ```
    $ netstat -tp
    Active Internet connections (w/o servers)
    Proto Recv-Q Send-Q Local Address               Foreign Address             State       PID/Program name
    tcp        0      0 192.168.0.2:ssh             192.168.0.1:egs             ESTABLISHED 2179/sshd
    tcp        1      0 192.168.0.2:59292           www.gov.com:http            CLOSE_WAIT  1939/clock-applet
    ```

## Displaying Promiscuous Mode
Displaying Promiscuous mode with ``-ac`` switch, netstat print the selected information or refresh screen every five second. Default screen refresh in every second.

    ```
    $ netstat -ac 5 | grep tcp
    tcp        0      0 *:sunrpc                    *:*                         LISTEN
    tcp        0      0 *:58642                     *:*                         LISTEN
    tcp        0      0 *:ssh                       *:*                         LISTEN
    tcp        0      0 localhost:ipp               *:*                         LISTEN
    tcp        0      0 localhost:smtp              *:*                         LISTEN
    tcp        1      0 192.168.0.2:59447           www.gov.com:http            CLOSE_WAIT
    tcp        0     52 192.168.0.2:ssh             192.168.0.1:egs             ESTABLISHED
    tcp        0      0 *:sunrpc                    *:*                         LISTEN
    tcp        0      0 *:ssh                       *:*                         LISTEN
    tcp        0      0 localhost:ipp               *:*                         LISTEN
    tcp        0      0 localhost:smtp              *:*                         LISTEN
    tcp        0      0 *:59482                     *:*                         LISTEN
    ...
    ```

## Displaying Kernel IP routing
Display Kernel IP routing table with netstat and route command.

    ```
    $ netstat -r
    Kernel IP routing table
    Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
    192.168.0.0     *               255.255.255.0   U         0 0          0 eth0
    link-local      *               255.255.0.0     U         0 0          0 eth0
    default         192.168.0.1     0.0.0.0         UG        0 0          0 eth0
    ```

## Showing Network Interface Transactions
Showing network interface packet transactions including both transferring and receiving packets with MTU size.

    ```
    $ netstat -i
    Kernel Interface table
    Iface      MTU    RX-OK RX-ERR RX-DRP RX-OVR    TX-OK TX-ERR TX-DRP TX-OVR Flg
    ens192    1500  9137408      0      0 0       6004161      0      0      0 BMRU
    lo       65536      926      0      0 0           926      0      0      0 LRU
    virbr0    1500        0      0      0 0             0      0      0      0 BMU
    virbr1    1500        0      0      0 0             0      0      0      0 BMU
    ```
##  Showing Kernel Interface Table
Showing Kernel interface table, similar to ifconfig command.

    ```
    $ netstat -ie
    Kernel Interface table
    ens192: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
            inet x.xxx.xxx.xxx  netmask 255.255.254.0  broadcast 9.151.193.255
            ether 00:50:56:bc:71:a4  txqueuelen 1000  (Ethernet)
            RX packets 9140039  bytes 7475704655 (6.9 GiB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 6005722  bytes 2286158472 (2.1 GiB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

    lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
            inet 127.0.0.1  netmask 255.0.0.0
            loop  txqueuelen 1  (Local Loopback)
            RX packets 926  bytes 67934 (66.3 KiB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 926  bytes 67934 (66.3 KiB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

    virbr0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
            inet 192.168.122.1  netmask 255.255.255.0  broadcast 192.168.122.255
            ether 00:16:3e:29:00:0b  txqueuelen 1000  (Ethernet)
            RX packets 0  bytes 0 (0.0 B)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 0  bytes 0 (0.0 B)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

    virbr1: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
            inet 192.168.123.1  netmask 255.255.255.0  broadcast 192.168.123.255
            ether 52:54:00:c2:a5:ad  txqueuelen 1000  (Ethernet)
            RX packets 0  bytes 0 (0.0 B)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 0  bytes 0 (0.0 B)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
    ```

## Displaying IPv4 and IPv6 Information
Displays multicast group membership information for both **IPv4** and **IPv6**.
    
    
    $ netstat -g
    IPv6/IPv4 Group Memberships
    Interface       RefCnt Group
    --------------- ------ ---------------------
    lo              1      all-systems.mcast.net
    eth0            1      224.0.0.251
    eth0            1      all-systems.mcast.net
    lo              1      ff02::1
    eth0            1      ff02::202
    eth0            1      ff02::1:ffb4:da21
    eth0            1      ff02::1
    

## Print Netstat Information Continuously
To get netstat information every few second, then use the following command, it will print netstat information continuously, say every few seconds.

    
    $ netstat -c
    Active Internet connections (w/o servers)
    Proto Recv-Q Send-Q Local Address               Foreign Address             State
    tcp        0      0 tecmint.com:http   sg2nlhg007.shr.prod.s:36944 TIME_WAIT
    tcp        0      0 tecmint.com:http   sg2nlhg010.shr.prod.s:42110 TIME_WAIT
    tcp        0    132 tecmint.com:ssh    115.113.134.3.static-:64662 ESTABLISHED
    tcp        0      0 tecmint.com:http   crawl-66-249-71-240.g:41166 TIME_WAIT
    tcp        0      0 localhost.localdomain:54823 localhost.localdomain:smtp  TIME_WAIT
    tcp        0      0 localhost.localdomain:54822 localhost.localdomain:smtp  TIME_WAIT
    tcp        0      0 tecmint.com:http   sg2nlhg010.shr.prod.s:42091 TIME_WAIT
    tcp        0      0 tecmint.com:http   sg2nlhg007.shr.prod.s:36998 TIME_WAIT
    ....
    

## Finding non supportive Address
Finding un-configured address families with some useful information.
    
    
    $ netstat --verbose
    netstat: no support for `AF IPX' on this system.
    netstat: no support for `AF AX25' on this system.
    netstat: no support for `AF X25' on this system.
    netstat: no support for `AF NETROM' on this system.
    

## Finding Listening Programs
Find out how many listening programs running on a port.

    
    # netstat -ap | grep http
    tcp        0      0 *:http                      *:*                         LISTEN      9056/httpd
    tcp        0      0 *:https                     *:*                         LISTEN      9056/httpd
    tcp        0      0 tecmint.com:http   sg2nlhg008.shr.prod.s:35248 TIME_WAIT   -
    tcp        0      0 tecmint.com:http   sg2nlhg007.shr.prod.s:57783 TIME_WAIT   -
    tcp        0      0 tecmint.com:http   sg2nlhg007.shr.prod.s:57769 TIME_WAIT   -
    tcp        0      0 tecmint.com:http   sg2nlhg008.shr.prod.s:35270 TIME_WAIT   -
    tcp        0      0 tecmint.com:http   sg2nlhg009.shr.prod.s:41637 TIME_WAIT   -
    tcp        0      0 tecmint.com:http   sg2nlhg009.shr.prod.s:41614 TIME_WAIT   -
    unix  2      [ ]         STREAM     CONNECTED     88586726 10394/httpd
    

## Displaying RAW Network Statistics

    
    $ netstat --statistics --raw
    Ip:
        7775262 total packets received
        0 forwarded
        0 incoming packets discarded
        7749641 incoming packets delivered
        6022556 requests sent out
        88 dropped because of missing route
    Icmp:
        2383 ICMP messages received
        0 input ICMP message failed.
        ICMP input histogram:
            destination unreachable: 2
            timeout in transit: 2175
            echo requests: 6
            echo replies: 200
        2889 ICMP messages sent
        0 ICMP messages failed
        ICMP output histogram:
            destination unreachable: 159
            echo request: 3
            echo replies: 6
    IcmpMsg:
            InType0: 200
            InType3: 2
            InType8: 6
            InType11: 2175
            OutType0: 6
            OutType3: 159
            OutType8: 3
            OutType69: 2721
    UdpLite:
    IpExt:
        InNoRoutes: 1
        InMcastPkts: 55171
        OutMcastPkts: 5239
        InBcastPkts: 217626
        InOctets: 7308786810
        OutOctets: 2203420447
        InMcastOctets: 50203190
        OutMcastOctets: 5090716
        InBcastOctets: 43650691
        InNoECTPkts: 8725502
    