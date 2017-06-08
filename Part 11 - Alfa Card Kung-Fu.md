#### Part 11: Alfa Card Kung-Fu

View kernel messages

```sh
root@kali:~# tail -f /var/log/messages
```

Getting the most out of the Alfa card

```sh
root@kali:~# ifconfig wlan0 down
root@kali:~# iw reg set BO
root@kali:~# ifconfig wlan0 up
root@kali:~# iwconfig wlan0 channel 12
root@kali:~# iwconfig wlan0 txpower 30
root@kali:~# iwconfig
wlan0     IEEE 802.11  ESSID:off/any
          Mode:Managed  Frequency:2.467 GHz  Access Point: Not-Associated
          Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:off

eth0      no wireless extensions.

lo        no wireless extensions.

root@kali:~#
```

```sh
root@kali:~# ifconfig wlan0 down
root@kali:~# iw reg set BZ
root@kali:~# iwconfig wlan0 channel 12
root@kali:~# iwconfig wlan0 txpower 30
root@kali:~# iwconfig
wlan0     IEEE 802.11  ESSID:off/any
          Mode:Managed  Frequency:2.467 GHz  Access Point: Not-Associated
          Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:off

eth0      no wireless extensions.

lo        no wireless extensions.

root@kali:~#
```
