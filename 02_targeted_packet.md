## airodump-ng & wireshark

**airodump-ng**

```
root@kali:~# airodump-ng wlan0

CH 12 ][ Elapsed: 17 mins ][ 2019-01-20 10:49                                         
                                                                                                                                                                                                                  
 BSSID              PWR  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID
 (MAC sddr)   (distance)  (?)  (捕捉到的封包數量)  (過去每十秒接收到的封包數量)...
 
  **:**:**:**:**:**  -40     2012     3471    0   1  130  WPA2 CCMP   PSK  home                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                   
 BSSID              STATION            PWR   Rate    Lost    Frames  Probe 
 ...
 
 
 // 針對特定 BSSID 收集:
 root@kali:~# airodump-ng --bssid **:**:**:**:**:** --channel 1 --write home_20190120 wlan0

 CH  1 ][ Elapsed: 15 mins ][ 2019-01-20 11:08                                         
                                                                                                                                                                                                                  
 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID
                                                                                                                                                                                                                  
 **:**:**:**:**:**  -36  93     8741    14844    0   1  130  WPA2 CCMP   PSK  home                                                                                                                                
                                                                                                                                                                                                                  
 BSSID              STATION            PWR   Rate    Lost    Frames  Probe                                                                                                                                        
                                                                                                                                                                                                                  
 **:**:**:**:**:**  **:**:**:**:**:##  -18    0e- 6e     0     8908                                                                                                                                                
...    

// Check files:
root@kali:~# ls
home_20190120-01.cap  home_20190120-01.csv  home_20190120-01.kismet.csv  home_20190120-01.kismet.netxml
```

Ref: https://blog.csdn.net/qq_28208251/article/details/47975161

Ref: https://www.ubuntu-tw.org/modules/newbb/viewtopic.php?topic_id=105922

**wireshark**

解析 cap 檔！
