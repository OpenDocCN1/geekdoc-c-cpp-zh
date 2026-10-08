```
CME_Voice(config-ephone-dn)# pickup-group 5509
CME_Voice(config-ephone-dn)# ephone-dn 4
CME_Voice(config-ephone-dn)# pickup-group 5510
CME_Voice(config-ephone-dn)# ephone-dn 5
CME_Voice(config-ephone-dn)# pickup-group 5510
CME_Voice(config-ephone-dn)# ephone-dn 6
CME_Voice(config-ephone-dn)# pickup-group 5510
```

Note: When you assign the first ephone-dn to a call group number, CME creates the call pickup group. No additional command is needed for the call pickup creation.

When you assign the ephone-dns to the respective call pickup groups, users can begin answering other ringing phones. CME permits three methods to answer other ringing phones:

+   **Directed pickup:** You can pick up another ringing phone directly by pressing the PickUp softkey and dialing the DN of the ringing phone. CME then transfers the call and immediately answers it at your local place.

+   **Local pickup:** You can pick up another ringing phone in the same call pickup group as your phone by pressing the GPickUp button and entering an asterisk (*) when you hear the second dial tone.

+   **Other group pickup:** You can pick up a ringing phone in another group by pressing the GPickUp button and entering the other group number when you hear the second dial tone.

If multiple phones are ringing in the user's call pickup group, CME answers the oldest ringing phone when the user invokes call pickup.

Note: The GPickUp softkey functions differently depending on the call pickup configuration in CME. If there is only one group configured in CME, the GPickUp button automatically answers the call from your group number. You will not hear a second dial tone, and you do not need to dial an asterisk to signify your group, because only one group is defined. After you configure multiple groups in CME, you hear a second dial tone after pressing the GPickUp softkey; at this point, you can dial either an asterisk for the local group or another group number.

Tip: By default, users can pick up other ringing phones managed by CME using the directed pickup method, described previously, regardless of the destination device being assigned to a Call Pickup group. To disable this feature, enter the command no service directed-pickup from telephony service configuration mode. After you enter this command, the GPickUp softkey on the IP phones operates as a local group button. Pressing the softkey immediately answers ringing calls in your own local pickup group.

![](bbox=[0.065, 0.415, 0.115, 0.465])