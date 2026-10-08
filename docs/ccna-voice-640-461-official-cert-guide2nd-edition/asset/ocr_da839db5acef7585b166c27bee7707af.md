After you enter the command ephone \<tag>, the CME router moves you into ephone configuration mode. Every command you enter after this directly affects the Cisco IP Phone matched to this.

After initially creating the ephone, you need to logically link it to the physical phone it represents. The CME router uses the MAC address of a Cisco IP Phone for this purpose. There are three ways to find the MAC address of a Cisco IP Phone:

+   - On the box of the Cisco IP Phone: The box the Cisco IP Phone ships has in the MAC address of the phone on next to a UPC code.

+   - On the back of the Cisco IP Phone: A sticker on the back side of the phone lists the MAC address of the device. The address appears next to a UPC code.

+   - From the Settings menu of Cisco IP Phone: All IP Phones have Settings button that enables you to manually configure various settings for the device. On most models of Cisco IP Phones, choosing Settings and then Network Configuration displays the MAC address of the phone on the LCD display.

> Note: A UPC code containing the MAC address information of the IP phone is beneficial if you have a handheld UPC scanner (barcode scanner). You can set the scanner to allow you to scan the MAC address of each device and then the extension number into an Excel spreadsheet. You can export this information for bulk entry of devices.

When you have the MAC address of the IP phone, you can enter it from ephone configuration mode, as shown in Example 5-7.

# Example 5-7 Assigning a MAC Address to an Ephone

```
CME_Voice(config)# ephone 1
CME_Voice(config-ephone)# mac-address ?
H.H.H Mac address
<cr>
CME_Voice(config-ephone)# mac-address 0014.1c48.e71a
```

![](bbox=[0.863, 0.611, 0.923, 0.663])

After you enter the ephone MAC address information, you can verify the IP phone registration status by using the show ephone command, shown in Example 5-8.

# Example 5-8 Verifying Ephone Registration Status

```
CME_Voice# show ephone
ephone-1 Mac:0014.1C48.E6D1 TCP socket:[2] activeLine:0 REGISTERED in SCCP ver 11\and Server in ver 8
mediaActive:0 offhook:0 ringing:0 reset:0 reset_sent:0 paging 0 debug:0 caps:8
IP:172.30.60.31 52777 Telecaster 7960 keepalive 0 max_line 6
```