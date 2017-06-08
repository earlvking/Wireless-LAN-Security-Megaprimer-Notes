#### Wi-Fi Challenge 1 (Level Easy) : There Is No Patch For Stupidity!

[Challenge Packet Trace](http://code.securitytube.net/Challenge-1-Easy)

Inspecting the file

```sh
root@kali:~# file Challenge-1-Easy
Challenge-1-Easy: tcpdump capture file (little-endian) - version 2.4 (802.11 with radiotap header, capture length 65535)
root@kali:~#
```

Try cracking using ```aircrack-ng```

```sh
root@kali:~# aircrack-ng Challenge-1-Easy
Opening Challenge-1-Easy
Read 3 packets.

   #  BSSID              ESSID                     Encryption

   1  00:21:91:D2:8E:25                            WEP (1 IVs)

Choosing first network as target.

Opening Challenge-1-Easy
Attack will be restarted every 5000 captured ivs.
Starting PTW attack with 1 ivs.

                                          Aircrack-ng 1.2 rc4


                          [00:00:00] Tested 0 keys (got 1 IVs)

   KB    depth   byte(vote)
    0  255/256   FF(   0) 00(   0) 01(   0) 02(   0) 04(   0) 05(   0) 06(   0)
    1    0/  7   D0( 256) 00(   0) 01(   0) 02(   0) 03(   0) 04(   0) 05(   0)
    2    0/  1   17( 256) 00(   0) 01(   0) 02(   0) 03(   0) 04(   0) 05(   0)
    3    0/  3   1D( 256) 00(   0) 01(   0) 02(   0) 03(   0) 04(   0) 05(   0)
    4    0/  4   C6( 256) 00(   0) 01(   0) 02(   0) 03(   0) 04(   0) 05(   0)

Failed. Next try with 5000 IVs.
^C
Quitting aircrack-ng...
root@kali:~#
```

Solution

```sh
root@kali:~# airdecap-ng -w AABBCCDDEE Challenge-1-Easy
Total number of packets read             3
Total number of WEP data packets         1
Total number of WPA data packets         0
Number of plaintext data packets         0
Number of decrypted WEP  packets         0
Number of corrupted WEP  packets         0
Number of decrypted WPA  packets         0
root@kali:~#
```

Need the ```WEP``` key of the target network in ```hex```

Script that

1. Opens the wordlist
2. Reads every line of the file
3. Perms through the file and looks for alpha numeric possibilities
4. Checks the size of the wepKey
5. Creates a hex equivalent of the string 
6. Runs ```airdecap-ng```
7. Checks the 5<sup>th</sup> line of the output and sees if that is greater than ```1```
8. If so then it prints the key

```python
#!/usr/bin/python
# Author - Vivek Ramachandran vivek@securitytube.net
#
# Solution to Challenge 1: http://www.securitytube.net/1856


import sys, binascii, re
from subprocess import Popen, PIPE

f = open(sys.argv[1], 'r')
for line in f:
	wepKey = re.sub(r'\W+', '', line)

	if len(wepKey) != 5 :
		continue

	hexKey = binascii.hexlify(wepKey)

	print "Trying with WEP Key: " +wepKey + " Hex: " + hexKey

	p = Popen(['airdecap-ng', '-w', hexKey, 'Challenge-1-Easy'], stdout=PIPE)
	output = p.stdout.read()

	finalResult = output.split('\n')[4]
	if finalResult.find('1') != -1 :
		print "Success WEP Key Found: "  + wepKey
		sys.exit(0)

print "Failure! WEP Key Could not be Found with the existing dictionary!"
```

Run the script

```sh
root@kali:~# ./Crack-1.py darkc0de.txt
Trying with WEP Key: 00000 Hex: 3030303030
Trying with WEP Key: 00119 Hex: 3030313139
Trying with WEP Key: 0012d Hex: 3030313264
Trying with WEP Key: 0014k Hex: 303031346b
Trying with WEP Key: 007id Hex: 3030376964
Trying with WEP Key: 00p0d Hex: 3030703064
Trying with WEP Key: 00p4k Hex: 303070346b
Trying with WEP Key: 01012 Hex: 3031303132
Trying with WEP Key: 01069 Hex: 3031303639
Trying with WEP Key: 010n4 Hex: 3031306e34
Trying with WEP Key: 011i3 Hex: 3031316933
Trying with WEP Key: 01210 Hex: 3031323130
<---snip--->
Trying with WEP Key: Tubin Hex: 547562696e
Trying with WEP Key: Tubis Hex: 5475626973
Trying with WEP Key: tuboy Hex: 7475626f79
Trying with WEP Key: tubvm Hex: 747562766d
Trying with WEP Key: tucan Hex: 747563616e
Trying with WEP Key: tucci Hex: 7475636369
Trying with WEP Key: Tucci Hex: 5475636369
Trying with WEP Key: TUCCI Hex: 5455434349
Trying with WEP Key: TUCEK Hex: 545543454b
Trying with WEP Key: tuchk Hex: 747563686b
Trying with WEP Key: tucke Hex: 7475636b65
Trying with WEP Key: tucks Hex: 7475636b73
Trying with WEP Key: tucky Hex: 7475636b79
Trying with WEP Key: Tucky Hex: 5475636b79
Trying with WEP Key: tucmd Hex: 7475636d64
Trying with WEP Key: tucom Hex: 7475636f6d
Trying with WEP Key: tucs1 Hex: 7475637331
Trying with WEP Key: tucul Hex: 747563756c
Trying with WEP Key: tudes Hex: 7475646573
Success WEP Key Found: tudes
root@kali:~# ls -l Challenge-1-Easy*
-rw-r--r-- 1 root root 858 May 12  2011 Challenge-1-Easy
-rw-r--r-- 1 root root 382 Jun  8 15:31 Challenge-1-Easy-dec
root@kali:~#
```