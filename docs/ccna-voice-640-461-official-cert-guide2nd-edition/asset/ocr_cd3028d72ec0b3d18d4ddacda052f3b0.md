To create pickup groups in CCP, navigate to the Call Pickup Groups configuration window (Unified Communications > Telephony Features > Call Pickup Groups) and click the Create button. The user-friendly configuration window allows you you to define the pickup group number and allocate which extensions you want to include in the pickup group, as shown in Figure 7-15.

![](bbox=[0.115, 0.185, 0.792, 0.597])

Figure 7-15 Configuring Call Pickup Groups in CCP

If you were to click the Deliver button with the CCP configuration shown in Figure 7-15, the CCP delivers the following commands to the Cisco router:

```
ephone-dn 2 dual-line
picking-group 1234
exit
ephone-dn 1 dual-line
picking-group 1234
exit
```

# Configuring Intercom

Intercom configurations are common in traditional phone systems. This feature allows an administrative assistant and executive to work closely together by having a speakerphone “tether” between them.