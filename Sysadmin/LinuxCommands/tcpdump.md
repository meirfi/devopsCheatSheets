
# Tcpdump Commands – A Network Sniffer Tool

# A TCPdump Tutorial and Primer with Examples


- What is TCPdump?
- How to Install tcpdump in Linux
- TCPdump Basics
- TCPdump basic command examples
    - Basic tcpdump Communication
    - specific interface
    - raw output view
    - find traffic by ip
    - seeing packet contents with hex output
    - filtering by source and/or destination
    - finding packets by network
    - show traffic related to a port
    - show traffic of one protocol
    - show only ip6 traffic
    - find traffic using port ranges
    - find traffic based on packet size
    - writing captures to a file
    - reading traffic from a file
 
- TCPdump advanced command 
    - it’s all about the combinations
    - from specific ip and destined for a specific port
    - from one network to another
    - non icmp traffic going to a specific ip
    - traffic from a host that isn’t on a specific port
    - complex grouping and special characters
    - isolating specific tcp flags
    - identifying noteworthy traffic
        - both syn and rst set
        - cleartext http gets
        - ssh connections
        - low ttl
        - evil bit set
- summary

### What tcpdump?
Tcpdump is the premier network analysis tool for information security professionals. <br>
Having a solid grasp of this über-powerful application is mandatory for anyone desiring a thorough understanding of TCP/IP. Many prefer to use higher level analysis tools such as Wireshark, but I believe this to usually be a mistake.

When using a tool that displays network traffic a more natural (raw) way the burden of analysis is placed directly on the human rather than the application.<br> This approach cultivates continued and elevated understanding of the TCP/IP suite, and for this reason I strongly advocate using tcpdump instead of other tools whenever possible.

```bash
15:31:34.079416 IP (tos 0x0, ttl 64, id 20244, offset 0, flags [DF], 
proto: TCP (6), length: 60) source.35970 > dest.80: S, cksum 0x0ac1 
(correct), 2647022145:2647022145(0) win 5840 0x0000: 4500 003c 4f14 
4006 7417 0afb 0257  E..  0x0010: 4815 222a 8c82 0050 9dc6 5a41 0000 
0000  H."*...P..ZA.... 0x0020: a002 16d0 0ac1 0000 0204 05b4 
0402 080a  ................ 0x0030: 14b4 1555 0000 0000 0103 0302
TABLE 1. — RAW TCP/IP OUTPUT.
```
### How to Install tcpdump in Linux
```bash
yum install tcpdump
```

### TCPdump Basics
Below are a few options you can use when configuring tcpdump.<br> They’re easy to forget and/or confuse with other types of filters, e.g., Wireshark, so hopefully this page can serve as a reference for you, as it does me. here are the main ones I like to keep in mind depending on what I’m looking at.


Options
- -i any : Listen on all interfaces just to see if you’re seeing any traffic.
- -i eth0 : Listen on the eth0 interface.
- -D : Show the list of available interfaces
- -n : Don’t resolve hostnames.
- -nn : Don’t resolve hostnames or port names.
- -q : Be less verbose (more quiet) with your output.
- -t : Give human-readable timestamp output.
- -tttt : Give maximally human-readable timestamp output.
- -X : Show the packet’s contents in both hex and ascii.
- -XX : Same as -X, but also shows the ethernet header.
- -v, -vv, -vvv : Increase the amount of packet information you get back.
- -c : Only get x number of packets and then stop.
- -s : Define the snaplength (size) of the capture in bytes. Use -s0 to get everything, unless you are intentionally capturing less.
- -S : Print absolute sequence numbers.
- -e : Get the ethernet header as well.
- -q : Show less protocol information.
- -E : Decrypt IPSEC traffic by providing an encryption key.
- The default snaplength as of tcpdump 4.0 has changed from 68 bytes to 96 bytes. While this will give you more of a packet to see, it still won’t get everything. Use -s 1514 or -s 0 to get full coverage.

## Expressions
In **tcpdump**, Expressions allow you to trim out various types of traffic and find exactly what you’re looking for. Mastering the expressions and learning to combine them creatively is what makes one truly powerful with **tcpdump**.

There are three main types of expression: ```type```, ```dir```, and ```proto```.
- Type options are: host, net, and port.
- Direction lets you do ```src```, ```dst```, and combinations thereof.
- Proto(col) lets you designate: ``tcp``, ``udp``, ``icmp``, ``ah``, and many more.

So, now that we’ve seen what our options are, let’s look at some real-world examples that we’re likely to see in our everyday work.

## TCPdump basic command examples
###  Display Available Interfaces
- To list number of available interfaces on the system, run the following command with ``-D`` option.
    ```bash
    $ tcpdump -D
    1.eth0
    2.eth1
    3.usbmon1 (USB bus number 1)
    4.usbmon2 (USB bus number 2)
    8.any (Pseudo-device that captures on all interfaces)
    9.lo
    ```
### Basic tcpdump Communication

- Just see what’s going on, by looking at all interfaces.
    ```bash
    $ tcpdump -i any
    ```

### Specific Interface
- Basic view of what’s happening on a particular interface.
    ```bash
    $ tcpdump -i eth0
    ```
    output:
    ```bash
    tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
    listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
    11:33:31.976358 IP 172.16.25.126.ssh > 172.16.25.125.apwi-rxspooler: Flags [P.], seq 3500440357:3500440553, ack 3652628334, win 18760, length 196
    11:33:31.976603 IP 172.16.25.125.apwi-rxspooler > 172.16.25.126.ssh: Flags [.], ack 196, win 64487, length 0
    11:33:31.977243 ARP, Request who-has tecmint.com tell 172.16.25.126, length 28
    11:33:31.977359 ARP, Reply tecmint.com is-at 00:14:5e:67:26:1d (oui Unknown), length 46
    11:33:31.977367 IP 172.16.25.126.54807 > tecmint.com: 4240+ PTR? 125.25.16.172.in-addr.arpa. (44)
    11:33:31.977599 IP tecmint.com > 172.16.25.126.54807: 4240 NXDomain 0/1/0 (121)
    11:33:31.977742 IP 172.16.25.126.44519 > tecmint.com: 40988+ PTR? 126.25.16.172.in-addr.arpa. (44)
    11:33:32.028747 IP 172.16.20.33.netbios-ns > 172.16.31.255.netbios-ns: NBT UDP PACKET(137): QUERY; REQUEST; BROADCAST
    11:33:32.112045 IP 172.16.21.153.netbios-ns > 172.16.31.255.netbios-ns: NBT UDP PACKET(137): QUERY; REQUEST; BROADCAST
    11:33:32.115606 IP 172.16.21.144.netbios-ns > 172.16.31.255.netbios-ns: NBT UDP PACKET(137): QUERY; REQUEST; BROADCAST
    11:33:32.156576 ARP, Request who-has 172.16.16.37 tell old-oraclehp1.midcorp.mid-day.com, length 46
    11:33:32.348738 IP tecmint.com > 172.16.25.126.44519: 40988 NXDomain 0/1/0 (121)
    ```
### Capture Only N Number of Packets
- When you run tcpdump command it will capture all the packets for specified interface, until you Hit cancel button.<br> But using ``-c`` option, you can capture specified number of packets. The below example will only capture 6 packets.
    
    ```bash
    $ tcpdump -c 5 -i eth0
    tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
    listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
    11:40:20.281355 IP 172.16.25.126.ssh > 172.16.25.125.apwi-rxspooler: Flags [P.], seq 3500447285:3500447481, ack 3652629474, win 18760, length 196
    11:40:20.281586 IP 172.16.25.125.apwi-rxspooler > 172.16.25.126.ssh: Flags [.], ack 196, win 65235, length 0
    11:40:20.282244 ARP, Request who-has tecmint.com tell 172.16.25.126, length 28
    11:40:20.282360 ARP, Reply tecmint.com is-at 00:14:5e:67:26:1d (oui Unknown), length 46
    11:40:20.282369 IP 172.16.25.126.53216 > tecmint.com.domain: 49504+ PTR? 125.25.16.172.in-addr.arpa. (44)
    11:40:20.332494 IP tecmint.com.netbios-ssn > 172.16.26.17.nimaux: Flags [P.], seq 3058424861:3058424914, ack 693912021, win 64190, length 53 NBT Session Packet: Session Message
    6 packets captured
    23 packets received by filter
    0 packets dropped by kernel
    ```
### Print Captured Packets in ASCII
- The below tcpdump command with option ``-A`` displays the package in **ASCII** format. It is a character-encoding scheme format.
    ```bash
    $ tcpdump -A -i eth0
    tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
    listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
    09:31:31.347508 IP 192.168.0.2.ssh > 192.168.0.1.nokia-ann-ch1: Flags [P.], seq 3329372346:3329372542, ack 4193416789, win 17688, length 196
    M.r0...vUP.E.X.......~.%..>N..oFk.........KQ..)Eq.d.,....r^l......m\.oyE....-....g~m..Xy.6..1.....c.O.@...o_..J....i.*.....2f.mQH...Q.c...6....9.v.gb........;..4.).UiCY]..9..x.)   ..Z.XF....'|..E......M..u.5.......ul
    09:31:31.347760 IP 192.168.0.1.nokia-ann-ch1 > 192.168.0.2.ssh: Flags [.], ack 196, win 64351, length 0
    M....vU.r1~P.._..........
    ^C09:31:31.349560 IP 192.168.0.2.46393 > b.resolvers.Level3.net.domain: 11148+ PTR? 1.0.168.192.in-addr.arpa. (42)
    E..F..@.@............9.5.2.f+............1.0.168.192.in-addr.arpa.....
    3 packets captured
    11 packets received by filter
    0 packets dropped by kernel
    ```

### Display Captured Packets in HEX and ASCII
- The following command with option ``-XX`` capture the data of each packet, including its link level header in **HEX** and **ASCII** format.

    ```bash
    $ tcpdump -XX -i eth0
    11:51:18.974360 IP 172.16.25.126.ssh > 172.16.25.125.apwi-rxspooler: Flags [P.], seq 3509235537:3509235733, ack 3652638190, win 18760, length 196
    0x0000:  b8ac 6f2e 57b3 0001 6c99 1468 0800 4510  ..o.W...l..h..E.
    0x0010:  00ec 8783 4000 4006 275d ac10 197e ac10  ....@.@.']...~..
    0x0020:  197d 0016 1129 d12a af51 d9b6 d5ee 5018  .}...).*.Q....P.
    0x0030:  4948 8bfa 0000 0e12 ea4d 22d1 67c0 f123  IH.......M".g..#
    0x0040:  9013 8f68 aa70 29f3 2efc c512 5660 4fe8  ...h.p).....V`O.
    0x0050:  590a d631 f939 dd06 e36a 69ed cac2 95b6  Y..1.9...ji.....
    0x0060:  f8ba b42a 344b 8e56 a5c4 b3a2 ed82 c3a1  ...*4K.V........
    0x0070:  80c8 7980 11ac 9bd7 5b01 18d5 8180 4536  ..y.....[.....E6
    0x0080:  30fd 4f6d 4190 f66f 2e24 e877 ed23 8eb0  0.OmA..o.$.w.#..
    0x0090:  5a1d f3ec 4be4 e0fb 8553 7c85 17d9 866f  Z...K....S|....o
    0x00a0:  c279 0d9c 8f9d 445b 7b01 81eb 1b63 7f12  .y....D[{....c..
    0x00b0:  71b3 1357 52c7 cf00 95c6 c9f6 63b1 ca51  q..WR.......c..Q
    0x00c0:  0ac6 456e 0620 38e6 10cb 6139 fb2a a756  ..En..8...a9.*.V
    0x00d0:  37d6 c5f3 f5f3 d8e8 3316 d14f d7ab fd93  7.......3..O....
    0x00e0:  1137 61c1 6a5c b4d1 ddda 380a f782 d983  .7a.j\....8.....
    0x00f0:  62ff a5a9 bb39 4f80 668a                 b....9O.f.
    11:51:18.974759 IP 172.16.25.126.60952 > mddc-01.midcorp.mid-day.com.domain: 14620+ PTR? 125.25.16.172.in-addr.arpa. (44)
    0x0000:  0014 5e67 261d 0001 6c99 1468 0800 4500  ..^g&...l..h..E.
    0x0010:  0048 5a83 4000 4011 5e25 ac10 197e ac10  .HZ.@.@.^%...~..
    0x0020:  105e ee18 0035 0034 8242 391c 0100 0001  .^...5.4.B9.....
    0x0030:  0000 0000 0000 0331 3235 0232 3502 3136  .......125.25.16
    0x0040:  0331 3732 0769 6e2d 6164 6472 0461 7270  .172.in-addr.arp
    0x0050:  6100 000c 0001                           a.....
    ```
### raw output view
- Verbose output, with no resolution of hostnames or port numbers, absolute sequence numbers, and human-readable timestamps.
    ```bash
    $ tcpdump -ttttnnvvS
    ```
### find traffic by ip
- One of the most common queries, this will show you traffic from 1.2.3.4, whether it’s the source or the destination.
    ```bash
    $ tcpdump host 1.2.3.4
    ```
### Seeing more of the packet with hex output
Hex output is useful when you want to see the content of the packets in question, and it’s often best used when you’re isolating a few candidates for closer scrutiny.
```bash
$ tcpdump -nnvXSs 0 -c1 icmp
```
output :
```bash
tcpdump: listening on eth0, link-type EN10MB (Ethernet), 23:11:10.370321 IP 
(tos 0x20, ttl  48, id 34859, offset 0, flags [none], length: 84) 
69.254.213.43 > 72.21.34.42: icmp 64: echo request seq 0 
        0x0000:  4520 0054 882b 0000 3001 7cf5 45fe d52b  E..T.+..0.|.E..+
        0x0010:  4815 222a 0800 3530 272a 0000 25ff d744  H."..50'..%..D
        0x0020:  ae5e 0500 0809 0a0b 0c0d 0e0f 1011 1213  .^..............
        0x0030:  1415 1617 1819 1a1b 1c1d 1e1f 2021 2223  .............!"#
        0x0040:  2425 2627 2829 2a2b 2c2d 2e2f 3031 3233  $%&'()*+,-./0123
        0x0050:  3435 3637                                4567
1 packets captured
1 packets received by filter
0 packets dropped by kernel
```

### Filtering by Source and Destination
It’s quite easy to isolate traffic based on either source or destination using src and dst.
    ```bash
    $ tcpdump src 2.3.4.5 
    $ tcpdump dst 3.4.5.6
    ```
### Finding Packets by Network
To find packets going to or from a particular network, use the net option. You can combine this with the src or dst options as well.
```bash
$ tcpdump net 1.2.3.0/24
```
### show traffic related to a specific port
You can find specific port traffic by using the port option followed by the port number.

```bash
$ tcpdump port 3389 
$ tcpdump src port 1025
```

### Show traffic of one protocol
If you’re looking for one particular kind of traffic, you can use tcp, udp, icmp, and many others as well.
```bash
$ tcpdump icmp
```
### Show only ip6 traffic
You can also find all IP6 traffic using the protocol option.
```bash
$ tcpdump ip6
```
### find traffic using port ranges
You can also use a range of ports to find traffic.
```bash
$ tcpdump portrange 21-23
```
### Find traffic based on packet size
If you’re looking for packets of a particular size you can use these options.<br>
You can use **less**, **greater**, or their associated symbols that you would expect from mathematics.
```bash
$ tcpdump less 32 
$ tcpdump greater 64 
$ tcpdump <= 128
```
### Writing Captures to a file
It’s often useful to save packet captures into a file for analysis in the future.<br> These files are known as PCAP (PEE-cap) files, and they can be processed by hundreds of different applications, including network analyzers, intrusion detection systems, and of course by tcpdump itself.<br>
Here we’re writing to a file called capture_file using the ``-w`` switch.
```bash
$ tcpdump port 80 -w capture_file
```
### Reading pcap files
You can read PCAP files by using the ``-r`` switch. <br>Note that you can use all the regular commands within tcpdump while reading in a file; you’re only limited by the fact that you can’t capture and process what doesn’t exist in the file already.
```bash
$ tcpdump -r capture_file
```
### Capture and Save Packets in a File
- As we said, that tcpdump has a feature to capture and save the file in a .pcap format, to do this just execute command with ``-w`` option.
    ```bash
    $ tcpdump -w 0001.pcap -i eth0
    tcpdump: listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
    4 packets captured
    4 packets received by filter
    0 packets dropped by kernel
    ```
### Read Captured Packets File
- To read and analyze captured packet 0001.pcap file use the command with -r option, as shown below.
    ```bash
    $ tcpdump -r 0001.pcap
    reading from file 0001.pcap, link-type EN10MB (Ethernet)
    09:59:34.839117 IP 192.168.0.2.ssh > 192.168.0.1.nokia-ann-ch1: Flags [P.], seq 3353041614:3353041746, ack 4193563273, win 18760, length 132
    09:59:34.963022 IP 192.168.0.1.nokia-ann-ch1 > 192.168.0.2.ssh: Flags [.], ack 132, win 65351, length 0
    09:59:36.935309 IP 192.168.0.1.netbios-dgm > 192.168.0.255.netbios-dgm: NBT UDP PACKET(138)
    09:59:37.528731 IP 192.168.0.1.nokia-ann-ch1 > 192.168.0.2.ssh: Flags [P.], seq 1:53, ack 132, win 65351, length 5
    1. Capture IP address Packets
    ```
# Capture IP address Packets
- To capture packets for a specific interface, run the following command with option -n.

    ```bash
    $ tcpdump -n -i eth0
    tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
    listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
    12:07:03.952358 IP 172.16.25.126.ssh > 172.16.25.125.apwi-rxspooler: Flags [P.], seq 3509512873:3509513069, ack 3652639034, win 18760, length 196
    12:07:03.952602 IP 172.16.25.125.apwi-rxspooler > 172.16.25.126.ssh: Flags [.], ack 196, win 64171, length 0
    12:07:03.953311 IP 172.16.25.126.ssh > 172.16.25.125.apwi-rxspooler: Flags [P.], seq 196:504, ack 1, win 18760, length 308
    12:07:03.954288 IP 172.16.25.126.ssh > 172.16.25.125.apwi-rxspooler: Flags [P.], seq 504:668, ack 1, win 18760, length 164
    12:07:03.954502 IP 172.16.25.125.apwi-rxspooler > 172.16.25.126.ssh: Flags [.], ack 668, win 65535, length 0
    12:07:03.955298 IP 172.16.25.126.ssh > 172.16.25.125.apwi-rxspooler: Flags [P.], seq 668:944, ack 1, win 18760, length 276
    12:07:03.955425 IP 172.16.23.16.netbios-ns > 172.16.31.255.netbios-ns: NBT UDP PACKET(137): REGISTRATION; REQUEST; BROADCAST
    12:07:03.956299 IP 172.16.25.126.ssh > 172.16.25.125.apwi-rxspooler: Flags [P.], seq 944:1236, ack 1, win 18760, length 292
    12:07:03.956535 IP 172.16.25.125.apwi-rxspooler > 172.16.25.126.ssh: Flags [.], ack 1236, win 64967, length 0
    ```
#### Capture only TCP Packets.
- To capture packets based on TCP port, run the following command with option tcp.
    ```bash
    # tcpdump -i eth0 tcp
    tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
    listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
    12:10:36.216358 IP 172.16.25.126.ssh > 172.16.25.125.apwi-rxspooler: Flags [P.], seq 3509646029:3509646225, ack 3652640142, win 18760, length 196
    12:10:36.216592 IP 172.16.25.125.apwi-rxspooler > 172.16.25.126.ssh: Flags [.], ack 196, win 64687, length 0
    12:10:36.219069 IP 172.16.25.126.ssh > 172.16.25.125.apwi-rxspooler: Flags [P.], seq 196:504, ack 1, win 18760, length 308
    12:10:36.220039 IP 172.16.25.126.ssh > 172.16.25.125.apwi-rxspooler: Flags [P.], seq 504:668, ack 1, win 18760, length 164
    12:10:36.220260 IP 172.16.25.125.apwi-rxspooler > 172.16.25.126.ssh: Flags [.], ack 668, win 64215, length 0
    12:10:36.222045 IP 172.16.25.126.ssh > 172.16.25.125.apwi-rxspooler: Flags [P.], seq 668:944, ack 1, win 18760, length 276
    12:10:36.223036 IP 172.16.25.126.ssh > 172.16.25.125.apwi-rxspooler: Flags [P.], seq 944:1108, ack 1, win 18760, length 164
    12:10:36.223252 IP 172.16.25.125.apwi-rxspooler > 172.16.25.126.ssh: Flags [.], ack 1108, win 65535, length 0
    12:10:36.223461 IP mid-pay.midcorp.mid-day.com.netbios-ssn > 172.16.22.183.recipe: Flags [.], seq 283256512:283256513, ack 550465221, win 65531, length 1[|SMB]
    ```

## TCPdump advanced command
Now that we’ve seen what we can do with the basics tcpdump command through some examples, let’s look at some more advanced stuff.<br>

it’s all about the combinations
Being able to do these various things individually is powerful, but the real magic of tcpdump comes from the ability to combine options in creative ways in order to isolate exactly what you’re looking for. There are three ways to do combinations, and if you’ve studied programming at all they’ll be pretty familar to you.

1. AND    - ``and`` or ``&&``
2. OR     - ``or`` or ``||``
3. EXCEPT - ``not`` or ``!``

Here are some examples of combined commands.

### from specific ip and destined for a specific port
Let’s find all traffic from 10.5.2.3 going to any host on port 3389.
```bash
tcpdump -nnvvS src 10.5.2.3 and dst port 3389
```
### From one network to another
Let’s look for all traffic coming from 192.168.x.x and going to the 10.x or 172.16.x.x networks, and we’re showing hex output with no hostname resolution and one level of extra verbosity.
```bash
tcpdump -nvX src net 192.168.0.0/16 and dst net 10.0.0.0/8 or 172.16.0.0/16
```
### NON ICMP traffic going to a specific ip
This will show us all traffic going to 192.168.0.2 that is not ICMP.
```bash
$ tcpdump dst 192.168.0.2 and src net and not icmp
```
### Traffic from a host that isn’t on a specific port
This will show us all traffic from a host that isn’t SSH traffic (assuming default port usage).
```bash
$ tcpdump -vv src mars and not dst port 22
```
As you can see, you can build queries to find just about anything you need. The key is to first figure out precisely what you’re looking for and then to build the syntax to isolate that specific type of traffic.

### complex grouping and special characters

Also keep in mind that when you’re building complex queries you might have to group your options using single quotes.<br> 
Single quotes are used in order to tell **tcpdump** to ignore certain special characters—in this case below the “( )” brackets.<br>
This same technique can be used to group using other expressions such as host, port, net, etc. Take a look at the command below.

#### Traffic that’s from 10.0.2.4 AND destined for ports 3389 or 22 (incorrect)
```bash
$ tcpdump src 10.0.2.4 and (dst port 3389 or 22)
```

If you tried to run this otherwise very useful command, you’d get an error because of the parenthesis. You can either fix this by escaping the parenthesis (putting a before each one), or by putting the entire command within single quotes:

#### Traffic that’s from 10.0.2.4 AND destined for ports 3389 or 22 (correct)
```bash
$ tcpdump 'src 10.0.2.4 and (dst port 3389 or 22)'
```
### Isolating Specific TCP Flags

You can also capture traffic based on specific TCP flag(s).<br>

> The filters below find these various packets because tcp[13] looks at offset 13 in the tcp header, the number represents the location within the byte, and the !=0 means that the flag in question is set to 1, i.e. it’s on.

- Show me all URGENT (**URG**) packets…
    ```bash
    $ tcpdump 'tcp[13] & 32!=0'
    ```
- Show me all ACKNOWLEDGE (**ACK**) packets…
    ```bash
    $ tcpdump 'tcp[13] & 16!=0'
    ```
- Show me all PUSH (**PSH**) packets…
    ```bash
    $ tcpdump 'tcp[13] & 8!=0'
    ```
- Show me all RESET (**RST**) packets…
    ```bash
    $ tcpdump 'tcp[13] & 4!=0'
    ```
- Show me all SYNCHRONIZE (**SYN**) packets…
    ```bash
    $ tcpdump 'tcp[13] & 2!=0'
    ```
- Show me all FINISH (**FIN**) packets…
    ```bash
    $ tcpdump 'tcp[13] & 1!=0'
    ```
- Show me all SYNCHRONIZE/ACKNOWLEDGE (**SYNACK**) packets…
    ```bash
    $ tcpdump 'tcp[13]=18'
    ```
> Only the PSH, RST, SYN, and FIN flags are displayed in tcpdump‘s flag field output.<br> URGs and ACKs are displayed, but they are shown elsewhere in the output rather than in the flags field.

As with most powerful tools, however, there are multiple ways to do things.<br> The example below shows another way to capture packets with specific TCP flags set.
```bash
$ tcpdump 'tcp[tcpflags] == tcp-syn'
```
> Capture RST Flags Using the tcpflags option…
```bash
$ tcpdump 'tcp[tcpflags] == tcp-rst'
```
> Capture FIN Flags Using the tcpflags option…
```bash
$ tcpdump 'tcp[tcpflags] == tcp-fin'
```
>The same technique can be used for the other flags as well; they have been omitted in the interest of space.

### Identifying noteworthy traffic

Finally, there are a few quick recipes you’ll want to remember for catching specific and specialized traffic, such as malformed / likely-malicious packets.

##### packets with both the rst and syn flags set (this should never be the case)
```bash
$ tcpdump 'tcp[13] = 6'
```
##### find cleartext http get requests
```bash
$ tcpdump 'tcp[32:4] = 0x47455420'
```
##### find ssh connections on any port (via banner text)
```bash
$ tcpdump 'tcp[(tcp[12]>>2):4] = 0x5353482D'
```
##### packets with a ttl less than 10 (usually indicates a problem or use of traceroute)
```bash
$ tcpdump 'ip[8] < 10'
```
##### packets with the evil bit set (hacker trivia more than anything else)
```bash
$ tcpdump 'ip[6] & 128 != 0'
```

Summary

1. tcpdump is a valuable tool for anyone looking to get into networking or information security.
2. The raw way it interfaces with traffic, combined with the precision it offers in inspecting packets make it the best possible tool for learning TCP/IP.
3. Protocol Analyzers like Wireshark are great, but if you want to truly master packet-fu, you must become one with tcpdump first.

Well, this primer should get you going strong, but the man page should always be handy for the most advanced and one-off usage scenarios. I truly hope this has been useful to you, and feel free to contact me if you have any questions.
