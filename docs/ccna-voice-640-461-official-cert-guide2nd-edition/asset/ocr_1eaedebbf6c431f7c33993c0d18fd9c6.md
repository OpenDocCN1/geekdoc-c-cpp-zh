```
REMOTE_RTR(config)# dial-peer voice 11 pots
REMOTE_RTR(config-dial-peer#) destination-pattern 9911
REMOTE_RTR(config-dial-peer#) port 1/0/0
REMOTE_RTR(config-dial-peer#) forward-digits 3
REMOTE_RTR(config-dial-peer#) exit
REMOTE_RTR(config)# dial-peer voice 12 pots
REMOTE_RTR(config-dial-peer#) destination-pattern 911
REMOTE_RTR(config-dial-peer#) port 1/0/1
REMOTE_RTR(config-dial-peer#) no digit-strip
REMOTE_RTR(config-dial-peer#) exit
REMOTE_RTR(config)# dial-peer voice 13 pots
REMOTE_RTR(config-dial-peer#) destination-pattern 6911
REMOTE_RTR(config-dial-peer#) port 1/0/1
REMOTE_RTR(config-dial-peer#) forward-digits 3
```

![](bbox=[0.145, 0.395, 0.995, 0.93])

Figure 6-14 Centralizing PSTN Access