Bob's phone was "Bob Loblow" as the entry, Ethan's phone displays the caller as Bob Loblow.

+   - Line Text Label: This is the text that displays on the phone to describe the line; for example, if the second button on the phone is the shared DN for the Parts Desk, the Line Text Label for Line 2 might read "Parts Line."

+   - External Phone Number Mask: If this phone makes an off-net call (typically to the PSTN), this field can change the Calling Line ID (CLID) to present a full PSTN number instead of the internal DN.

+   7. Click Save.

+   8. In the Related Links drop-down, select Configure Device (<Phone>), and then click Go.

+   9. You are now at the Phone Configuration page for the new phone. At this point, if you need to continue making config changes you can do so, or you can click Save the changes so far. The page prompts to "Click on the Apply Config button to have the changes effect." This happens in order for the phone to adopt the changes, it has to reload with its new config. This requires either a Restart or a Reset, depending on what was changed.

> There is a great deal of confusion about Restart, Reset, and Apply Config. The differences are explained in the following points:

+   - A Reset reboots the firmware and the configuration of the phone. Some information such as firmware version, local changes, SRST, or Communications Manager Groups require a full reset so that the phone will pull a new page from the TFTP server. A Reset is triggered from the Administration web page, or from the phone itself by entering Settings >## (using the keypad).

+   - A Restart restarts the phone, and the phone comes right back and registers again. Because Communications Manager reads the database for this device when it registers, it is a good way to refresh information that is not passed through the configuration button. But changes, names, and forwarding would only require a Restart. A Restart is faster than a Reset, because the firmware is not rebooted at all.

+   - The confusion between Restart and Reset was that in CUCM 8.X, a new function labeled "Apply Config" was introduced. This button intelligently triggers either a Reset or a Restart as appropriate, depending on what changes were made to the device. In all cases, the phone has to be registered for the Reset or Restart to be sent to the phone.

It is common, especially with advanced features as Extension Mobility or Cisco Unified Personal Communications, to associate a user with a particular Device (IP Phone). It is required to associate the user with the Device if you want to be able to use the User Web Pages to customize their phone. The End User is associated with the Device (IP Phone), and the Device is associated with one or more DNs. This allows the user not only to access the User Web Pages to configure this phone, but for other applications and processes to interact with the user through the phone system.