#### Part 2 - Bands, Channels and	Sniffing	
Connect the Alfa card

```sh
root@kali:~# ifconfig 
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.0.101  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::a00:27ff:feec:26e5  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:ec:26:e5  txqueuelen 1000  (Ethernet)
        RX packets 2793  bytes 188729 (184.3 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 184  bytes 34264 (33.4 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1  (Local Loopback)
        RX packets 24  bytes 1272 (1.2 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 24  bytes 1272 (1.2 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlan0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether 3a:7e:d3:3f:0f:e8  txqueuelen 1000  (Ethernet)
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

phy2	wlan0		rtl8187		Realtek Semiconductor Corp. RTL8187

root@kali:~#

root@kali:~# airmon-ng start wlan0


PHY	Interface	Driver		Chipset

phy2	wlan0		rtl8187		Realtek Semiconductor Corp. RTL8187

		(mac80211 monitor mode vif enabled for [phy2]wlan0 on [phy2]wlan0mon)
		(mac80211 station mode vif disabled for [phy2]wlan0)
		
root@kali:~#

root@kali:~# airmon-ng 

PHY	Interface	Driver		Chipset

phy2	wlan0mon	rtl8187		Realtek Semiconductor Corp. RTL8187

root@kali:~# 
```

Check for the monitor mode interface

```sh
root@kali:~# ifconfig 
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.0.101  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::a00:27ff:feec:26e5  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:ec:26:e5  txqueuelen 1000  (Ethernet)
        RX packets 3859  bytes 254928 (248.9 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 216  bytes 39681 (38.7 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1  (Local Loopback)
        RX packets 24  bytes 1272 (1.2 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 24  bytes 1272 (1.2 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlan0mon: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        unspec 00-C0-CA-92-3C-89-30-30-00-00-00-00-00-00-00-00  txqueuelen 1000  (UNSPEC)
        RX packets 17753  bytes 3760300 (3.5 MiB)
        RX errors 0  dropped 17753  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

root@kali:~# 

root@kali:~# iwconfig 
wlan0mon  IEEE 802.11  Mode:Monitor  Frequency:2.457 GHz  Tx-Power=20 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          
eth0      no wireless extensions.

lo        no wireless extensions.

root@kali:~# 
```

Put the card on channel 1

```sh
root@kali:~# iwconfig
wlan0mon  IEEE 802.11  Mode:Monitor  Frequency:2.457 GHz  Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on

eth0      no wireless extensions.

lo        no wireless extensions.

root@kali:~# iwconfig wlan0mon channel 1
root@kali:~# iwconfig
wlan0mon  IEEE 802.11  Mode:Monitor  Frequency:2.412 GHz  Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on

eth0      no wireless extensions.

lo        no wireless extensions.

root@kali:~#
```

Make the card hop different channels and look for what is available in the air
<br/>
The value of <b>CH</b> keeps changing as the card hops various channels

```sh
root@kali:~# airodump-ng --band bg wlan0mon

 CH  1 ][ Elapsed: 6 s ][ 2017-06-05 01:55

 BSSID              PWR  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 3A:A0:97:B3:9B:A1  -64        2        0    0  11  54e. WPA2 CCMP   MGT  <length:  0>
 0A:A0:97:B3:9B:A1  -62        2        0    0  11  54e. OPN              xfinitywifi
 44:32:C8:2A:F1:02   -1        0        0    0   1  -1                    <length:  0>
 78:F2:9E:D2:F3:39  -24        3        0    0   6  54e. WPA2 CCMP   PSK  <length:  0>
 78:F2:9E:D2:F3:3B  -30        7        0    0   6  54e. OPN              <length:  0>
 78:F2:9E:D2:F3:3D  -26        5        0    0   6  54e. WPA2 CCMP   MGT  <length:  0>
 78:F2:9E:D2:F3:38  -29        6        0    0   6  54e. WPA2 CCMP   PSK  HOME-27B0-2.4
 FA:8F:CA:73:C0:80  -53        7        0    0   1  54e. OPN              <length:  0>
 AE:34:26:8A:34:A2  -38        4        0    0   1  54e. OPN              xfinitywifi
 9E:34:26:8A:34:A2  -38        2        0    0   1  54e. WPA2 CCMP   PSK  <length:  0>
 BE:34:26:8A:34:A2  -39        3        0    0   1  54e. WPA2 CCMP   PSK  <length:  0>
 9C:34:26:8A:34:A2  -38        4        0    0   1  54e. WPA2 CCMP   PSK  eeshawifi
 36:1F:E4:E5:52:91  -38        7        0    0  11  54e. WPA2 CCMP   PSK  <length:  0>
 84:C9:B2:6D:0C:85  -52        9        0    0   1  54e. OPN              dlink
 C4:04:15:3A:8B:30  -42        3        0    0   1  54e  WPA2 CCMP   PSK  NETGEAR43
 A0:63:91:4B:42:82  -40        7        2    0   3  54e  WPA2 CCMP   PSK  NETGEAR91
 46:1F:E4:E5:52:91  -41        9        0    0  11  54e. OPN              xfinitywifi
 34:97:F6:08:DB:18  -49        3        1    0  10  54e  WPA2 CCMP   PSK  IZZY
 34:1F:E4:E5:52:91  -38        6        0    0  11  54e. WPA2 CCMP   PSK  Lowspeed
 76:1F:E4:E5:52:91  -52        8        0    0  11  54e. WPA2 CCMP   MGT  <length:  0>
 AE:34:26:EE:C3:D6  -49        0        3    1   9  -1   OPN              <length:  0>
 78:F2:9E:D2:F3:3A  -46        7        0    0   6  54e. OPN              xfinitywifi
 FA:8F:CA:83:24:94  -57        5        0    0   7  54e. OPN              <length:  0>
 56:1F:E4:E5:52:91  -48        5        0    0  11  54e. WPA2 CCMP   PSK  <length:  0>
 B0:7F:B9:2A:4F:BB  -55        4        0    0  11  54e  WPA2 CCMP   PSK  kukikikukiki
 F8:ED:A5:BF:85:C0  -58        2        0    0   6  54e  WPA2 CCMP   PSK  HOME-85C2
 B0:7F:B9:71:19:9B  -58        3        0    0   6  54e  WPA2 CCMP   PSK  NETGEAR13
 C6:3F:B4:87:66:10  -59        2        0    0   1  54e  OPN              xfinitywifi
 C2:3F:B4:87:66:10  -60        4        0    0   1  54e  WPA2 CCMP   PSK  <length:  0>
 10:0D:7F:5F:FB:D2  -61        3        0    0  11  54e. WPA2 CCMP   PSK  NETGEAR72
 3C:36:E4:32:F7:C0  -62        3        1    0  11  54e  WPA2 CCMP   PSK  ATT016
 1A:A0:97:B3:9B:A1  -66        3        0    0  11  54e. WPA2 CCMP   PSK  <length:  0>

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

 44:32:C8:2A:F1:02  F4:5C:89:B7:7A:0D  -68    0 - 1e     0        6
 AE:34:26:EE:C3:D6  28:ED:6A:F0:E9:F3   -1   11e- 0      0        3
 3C:36:E4:32:F7:C0  64:80:99:D7:8E:03  -57    0 - 9e     0        1

root@kali:~#
```

