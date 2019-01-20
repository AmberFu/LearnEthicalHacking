## Testing Monitor Mode:

>
> `# ifconfig wlan0 down`
>
> `# airmon-ng check kill`
>
> `# iwconfig wlan0 mode monitor`
>
> `# ifconfig wlan0 up`

```
root@kali:~# iwconfig
lo        no wireless extensions.

eth0      no wireless extensions.

wlan0     IEEE 802.11  ESSID:off/any  
          Mode:Managed  Access Point: Not-Associated   Tx-Power=18 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:off
          
root@kali:~# ifconfig wlan0 down
root@kali:~# airmon-ng check kill

Killing these processes:

  PID Name
  521 dhclient
  763 wpa_supplicant

root@kali:~# iwconfig
lo        no wireless extensions.

eth0      no wireless extensions.

wlan0     IEEE 802.11  ESSID:off/any  
          Mode:Managed  Access Point: Not-Associated   Tx-Power=18 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:off
          
root@kali:~# iwconfig wlan0 mode monitor
root@kali:~# ifconfig wlan0 up
root@kali:~# iwconfig
lo        no wireless extensions.

eth0      no wireless extensions.

wlan0     IEEE 802.11  Mode:Monitor  Frequency:2.412 GHz  Tx-Power=18 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:off
```
Other way to enabling monitor mode by using `airmon-ng`: [youtube](https://www.youtube.com/watch?v=wiIoR_0epvs&feature=youtu.be)

```
# ifconfig wlan0 down
# airmon-ng check kill
# airmon-ng start wlan0
```
