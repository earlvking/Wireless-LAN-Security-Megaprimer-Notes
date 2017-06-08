#### Wi-Fi Challenge 2 (Level - Intermediate) : Know Thy Packets

[Challenge Packet Trace](http://code.securitytube.net/Challenge2.cap)

Understanding the packet capture

![Image of Wireshark](https://github.com/Kan1shka9/Wireless-LAN-Security-Megaprimer-Notes/blob/master/images/challenge/ch_2_1.jpeg)

The timestamps are not accurate as there are -ve values in the ```Time``` column.

Fixing the timestamp

Present Configuration

Wireshark &rarr; View &rarr; Time Display Format &rarr; Seconds Since Beginning of Capture

![Image of Wireshark](https://github.com/Kan1shka9/Wireless-LAN-Security-Megaprimer-Notes/blob/master/images/challenge/ch_2_2.jpeg)

Change it to

Wireshark &rarr; View &rarr; Time Display Format &rarr; Date and Time of Day

![Image of Wireshark](https://github.com/Kan1shka9/Wireless-LAN-Security-Megaprimer-Notes/blob/master/images/challenge/ch_2_3.jpeg)

Now the packet capture is sorted

![Image of Wireshark](https://github.com/Kan1shka9/Wireless-LAN-Security-Megaprimer-Notes/blob/master/images/challenge/ch_2_4.jpeg)

Browsing through the packet capture, a logical breakup can be observed as there is a time gap of approximately ```2:30``` between the packets

![Image of Wireshark](https://github.com/Kan1shka9/Wireless-LAN-Security-Megaprimer-Notes/blob/master/images/challenge/ch_2_5.jpeg)

Segregating the packets into separate trace files

![Image of Wireshark](https://github.com/Kan1shka9/Wireless-LAN-Security-Megaprimer-Notes/blob/master/images/challenge/ch_2_6.jpeg)

Filters used :

```
frame.time <= "2011-05-14 02:34:09.348717"
frame.time >= "2011-05-14 02:34:09.348717"
```
![Image of Wireshark](https://github.com/Kan1shka9/Wireless-LAN-Security-Megaprimer-Notes/blob/master/images/challenge/ch_2_7.jpeg)
![Image of Wireshark](https://github.com/Kan1shka9/Wireless-LAN-Security-Megaprimer-Notes/blob/master/images/challenge/ch_2_8.jpeg)

Cracking the key using ```aircrack-ng```

```sh
root@kali:~# aircrack-ng trace1.pcap
Opening trace1.pcap
Read 65810 packets.

   #  BSSID              ESSID                     Encryption

   1  00:21:91:D2:8E:25  PwnMe                     WEP (22071 IVs)

Choosing first network as target.

Opening trace1.pcap
Attack will be restarted every 5000 captured ivs.
Starting PTW attack with 22071 ivs.

                                          Aircrack-ng 1.2 rc4


                          [00:00:01] Tested 9704 keys (got 22071 IVs)

   KB    depth   byte(vote)
    0   45/ 54   4E(24064) 55(24064) 66(24064) 69(24064) 81(24064) 98(24064) B4(24064)
    1    0/  7   30(30464) 92(27648) 26(27392) 5F(27136) DA(27136) 99(26880) 4C(26624)
    2    0/  1   6F(37376) 3C(29696) 1A(27648) 3E(27392) 6A(27392) 45(26880) 09(26624)
    3    0/  2   42(33536) 50(29696) BD(27904) B7(27392) C0(27392) 6B(27136) 6C(27136)
    4   11/ 13   AA(26368) A9(26112) D4(26112) 00(25856) 74(25856) C3(25856) 21(25600)

                     KEY FOUND! [ 4E:30:6F:42:7A ] (ASCII: N0oBz )
	Decrypted correctly: 100%


root@kali:~#
```

```Key-1``` extracted 

```sh
root@kali:~# aircrack-ng trace2.pcap
Opening trace2.pcap
Read 54434 packets.

   #  BSSID              ESSID                     Encryption

   1  00:21:91:D2:8E:25  PwnMe                     WEP (11290 IVs)

Choosing first network as target.

Opening trace2.pcap
Attack will be restarted every 5000 captured ivs.
Starting PTW attack with 11290 ivs.

                                          Aircrack-ng 1.2 rc4


                          [00:00:06] Tested 125441 keys (got 11290 IVs)

   KB    depth   byte(vote)
    0   14/ 20   A5(14080) 2E(13824) 34(13824) 93(13824) CF(13824) DC(13824) 01(13568)
    1   19/  1   E8(13568) 07(13312) 4B(13312) 64(13312) 77(13312) 7B(13312) 83(13312)
    2    6/ 15   36(15360) 33(15104) 97(15104) D6(14848) 56(14592) 8D(14592) B3(14592)
    3   15/  3   C8(14080) 12(13824) 3D(13824) 5A(13824) 6A(13824) 76(13824) AA(13824)
    4    5/ 23   C1(14848) 00(14592) 4C(14592) E8(14592) 4D(14336) 92(14336) BD(14336)

Failed. Next try with 15000 IVs.
^C
Quitting aircrack-ng...
root@kali:~#
```

Unable to extract ```Key-2``` using default parameters.

Specifying the key length as 64

``` -n <nbits> : WEP key length :  64/128/152/256/512```

```sh
root@kali:~# aircrack-ng trace2.pcap -n 64
Opening trace2.pcap
Read 54434 packets.

   #  BSSID              ESSID                     Encryption

   1  00:21:91:D2:8E:25  PwnMe                     WEP (11290 IVs)

Choosing first network as target.

Opening trace2.pcap
Attack will be restarted every 5000 captured ivs.
Starting PTW attack with 11290 ivs.

                                          Aircrack-ng 1.2 rc4


                          [00:00:00] Tested 561341 keys (got 11246 IVs)

   KB    depth   byte(vote)
    0    4/  9   59(14848) 76(14848) F2(14848) 08(14592) 5D(14592) 85(14336) 8C(14336)
    1    3/ 29   75(15104) 05(14336) D7(14336) 2A(14080) 42(14080) 62(14080) 98(14080)
    2    5/  7   56(15360) 1B(15104) 33(15104) 97(15104) D6(14848) 56(14592) 8D(14592)
    3   26/ 37   6D(13568) 98(13568) AD(13568) D4(13568) D9(13568) 08(13312) 2A(13312)
    4    0/  9   59(17152) ED(16640) 2E(15104) 93(14848) E9(14848) 41(14848) 80(14592)

                     KEY FOUND! [ 59:75:4D:6D:59 ] (ASCII: YuMmY )
	Decrypted correctly: 100%


root@kali:~#
```

```Key-2``` extracted
