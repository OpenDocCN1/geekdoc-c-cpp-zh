# 64 CCNA Voice 640-461 Official Cert Guide

time. These advantages make NTP the preferred clock-setting method. The accuracy of the clock on your device depends on the stratum number of the NTP server. A stratum 1 time server is one that has a radio or atomic clock directly attached. The device that receives its time from this server via NTP is considered a stratum 2 device. The device that receives its time from this stratum 2 device via NTP is considered a stratum 3 device, and so on. There are many publicly accessible stratum 2 and 3 (and even some stratum 1) on the internet.

Note: You can obtain a list of publicly accessible NTP servers at www.ntp.org.

After you obtain one or more NTP servers to use, you can configure NTP support on your Cisco devices using the syntax in Example 3-4.

# Example 3-4 Configuring a Cisco Router to Receive Time via NTP

```
WAN_RTR#configure terminal
WAN_RTR(config)#ntp server 64.209.210.20
WAN_RTR(config)#clock timezone ARIONA -7
```

The first command, ntp server <ip address>, configures your Cisco device to use the specified NTP server; 64.209.210.20 is one of many publicly accessible NTP servers. If this is the only command you enter, your device will set itself to the Universal Time Coordinated (UTC) time zone. To accurately adjust the time for your device, use the clock timezone <name><hours> command. The previous syntax example set the time for Arizona to -7 hours from UTC.

Now that we have configured the router to synchronize with an NTP server, we can verify the NTP associations and the current time and date using the commands shown in Example 3-5.

# Example 3-5 Verifying NTP Configurations

```
WAN_RTR#show ntp associations
address             ref clock st poll reach offset delay disp
*-64.209.210.20      138.231.108.126  3 14   6 377 65.5  2.84 7.6
 * master (synced), # master (unsynced), + selected, - candidate, - configured
WAN_RTR#show clock
11:25:48.542 CA1_Dst Dec 13 2010
```

The key information from the show ntp associations command is just to the left of the configured NTP server address. The asterisk indicates that your Cisco device has synchronized with this server. You can configure multiple NTP sources for redundancy, the Cisco device will only choose one master NTP server to use at a time.

After you configure the Cisco router to synchronize with an NTP server, you can configure it to provide date and time information to a CUCM server, which can provide provide date and time information to the Cisco IP Phones in your network. To allow other