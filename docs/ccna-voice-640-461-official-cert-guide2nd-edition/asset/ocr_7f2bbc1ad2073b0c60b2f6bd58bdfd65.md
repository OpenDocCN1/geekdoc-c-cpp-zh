FXS 0/0/0
x1101
FXS 0/0/1
CME_A
x1102

![](bbox=[0.105, 0.087, 0.439, 0.159])

# Figure 6-8 PLAR Configuration

# Example 6-13 FXS PLAR Configuration

```
CME_A(config)# voice-port 0/0/0
CME_A(config-voiceport)# connection ?nplar  Private Line Auto Rewinding
tie-line A tie line
tunk      A Straight Tie Line
CME_A(config-voiceport)# connection plar ?nWORD A string of digits including wild cards
tied dedicated tie to this number
CME_A(config-voiceport)# connection plar 1102
```

![](bbox=[0.863, 0.255, 0.943, 0.303])

The FXS voice port 0/0/0 is now hard-coded to dial the number 1102 as soon as a user lifts the handset.

PLAR can also be useful in a variety of other circumstances. One common scenario is using FXO connections to the PSTN, as shown in Figure 6-9.

Receptionist
x1500

![](bbox=[0.283, 0.626, 0.843, 0.693])

FXO 2/0/0
FXO 2/0/1
PSTN
CME_A

# Figure 6-9 FXO PSTN Connections

Although the destination-pattern command dial peer configuration mode is useful for dictating what can go out the FXO ports, it is not useful for handling what comes in the FXO ports. When the CME_A router in Figure 6-9 receives an incoming call from the PSTN, the call information sent from the PSTN carrier does not include dialed number information (This is known as Dialed Number Identification Service [DNIS].) It includes caller ID information (known as Automatic Number Identification [ANI]), but this does not help the router know where to send the call when it is received.