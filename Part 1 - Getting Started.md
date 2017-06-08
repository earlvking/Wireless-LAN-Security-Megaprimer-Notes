#### Part 1 - Getting Started

Make the Alfa card exclusive to our Kali machine

![Image of VirtualBox](https://github.com/Kan1shka9/Wireless-LAN-Security-Megaprimer-Notes/blob/master/images/part_1.jpeg)

Alfa card not connected

```sh
root@kali:~# ifconfig 
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.0.101  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::a00:27ff:feec:26e5  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:ec:26:e5  txqueuelen 1000  (Ethernet)
        RX packets 1265  bytes 95241 (93.0 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 141  bytes 26896 (26.2 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1  (Local Loopback)
        RX packets 24  bytes 1272 (1.2 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 24  bytes 1272 (1.2 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
root@kali:~# 
```

Alfa card connected

```sh
root@kali:~# ifconfig 
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.0.101  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::a00:27ff:feec:26e5  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:ec:26:e5  txqueuelen 1000  (Ethernet)
        RX packets 1305  bytes 97653 (95.3 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 144  bytes 27104 (26.4 KiB)
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
        ether be:a1:c3:fd:65:b8  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
root@kali:~# 
```

View installed drivers

```sh
root@kali:~# lsmod
Module                  Size  Used by
fuse                   90112  3
arc4                   16384  2
nfnetlink_queue        20480  0
nfnetlink_log          20480  0
nfnetlink              16384  2 nfnetlink_log,nfnetlink_queue
bluetooth             434176  0
vboxsf                 40960  0
rtl8187                36864  0
eeprom_93cx6           16384  1 rtl8187
mac80211              548864  1 rtl8187
vboxvideo              45056  3
cfg80211              446464  2 mac80211,rtl8187
ppdev                  20480  0
joydev                 20480  0
rfkill                 20480  5 bluetooth,cfg80211
intel_rapl_perf        16384  0
pcspkr                 16384  0
evdev                  20480  10
serio_raw              16384  0
ttm                    77824  1 vboxvideo
drm_kms_helper        114688  1 vboxvideo
drm                   253952  6 vboxvideo,ttm,drm_kms_helper
parport_pc             28672  0
vboxguest             200704  6 vboxsf,vboxvideo
parport                40960  2 parport_pc,ppdev
sg                     32768  0
snd_intel8x0           32768  4
snd_ac97_codec         98304  1 snd_intel8x0
ac97_bus               16384  1 snd_ac97_codec
battery                16384  0
snd_pcm                86016  2 snd_ac97_codec,snd_intel8x0
snd_timer              28672  1 snd_pcm
video                  32768  0
ac                     16384  0
button                 16384  0
snd                    57344  12 snd_ac97_codec,snd_timer,snd_intel8x0,snd_pcm
soundcore              16384  1 snd
binfmt_misc            20480  1
acpi_cpufreq           20480  0
tpm_tis                16384  0
tpm_tis_core           20480  1 tpm_tis
tpm                    36864  2 tpm_tis,tpm_tis_core
ip_tables              20480  0
x_tables               20480  1 ip_tables
autofs4                36864  2
ext4                  499712  1
crc16                  16384  2 bluetooth,ext4
jbd2                   77824  1 ext4
crc32c_generic         16384  0
fscrypto               24576  1 ext4
ecb                    16384  0
mbcache                16384  2 ext4
hid_generic            16384  0
usbhid                 45056  0
hid                    94208  2 hid_generic,usbhid
sr_mod                 24576  0
cdrom                  49152  1 sr_mod
sd_mod                 40960  3
ata_generic            16384  0
ohci_pci               16384  0
crc32_pclmul           16384  0
crc32c_intel           16384  2
aesni_intel            20480  0
aes_i586               20480  1 aesni_intel
xts                    16384  1 aesni_intel
lrw                    16384  1 aesni_intel
gf128mul               20480  2 lrw,xts
ablk_helper            16384  1 aesni_intel
cryptd                 20480  1 ablk_helper
ohci_hcd               45056  1 ohci_pci
ehci_pci               16384  0
ehci_hcd               65536  1 ehci_pci
psmouse               118784  0
ahci                   36864  2
libahci                28672  1 ahci
ata_piix               32768  0
usbcore               184320  6 usbhid,ehci_hcd,ohci_pci,ohci_hcd,rtl8187,ehci_pci
e1000                 118784  0
usb_common             16384  1 usbcore
i2c_piix4              20480  0
libata                192512  4 ahci,ata_piix,libahci,ata_generic
scsi_mod              180224  4 sd_mod,libata,sr_mod,sg
root@kali:~#
```

