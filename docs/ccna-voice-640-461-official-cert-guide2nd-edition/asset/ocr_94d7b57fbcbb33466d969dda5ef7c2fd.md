+   - no-mute: Mutes the intercom to answer with unmuted speakerphone rather than muted. Although this is beneficial to allow immediate two-way conversation, you run the risk of one side barring into existing conversations or background noise.

CCP can also configure Intercom functionality. To do this, navigate to Unified Communications > Telephony Features > Intercom and click the Create button. The configuration window shown in Figure 7-16 allows you to select the user and speed-dial button you want to assign Intercom functionality.

![](bbox=[0.098, 0.243, 0.804, 0.663])

Figure 7-16 Configuring Intercom in CCP

After you click the Deliver button, CCP applies the following syntax to the router. Notice that CCP also uses alpha-numeric speed dials to prevent other users from accessing the intercom functionality inadvertently:

```
ephone-dn 5
number A105002
description Intercom
intercom A105102 label "Intercom Paul"
```

```
ephone-dn 4
number A105102
description Intercom
```