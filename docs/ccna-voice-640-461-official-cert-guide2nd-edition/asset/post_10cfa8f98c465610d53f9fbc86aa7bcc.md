
Thankfully, Cisco does not leave you “hoping” that the translation rule will work properly after it is applied to the interface. You can use the test voice translation-rule command from privileged mode to test the rules you create before you apply them, as shown in Example 6-22.

### Example 6-22 Testing Translation Rules

```
HQ_RTR# test voice translation-rule 1 6546
Matched with rule 1
Original number: 6546 Translated number: 5546
Original type: none Translated number type: none
Original plan: none Translated number plan: none
H_RTR# test voice translation-rule 1 6677
Matched with rule 1
Original number: 6677 Translated number: 5677
Original type: none Translated number type: none
Original plan: none Translated number plan: none
```

Example 6-22's output indicates the translation rule tests successfully, 6546 is translated to 5546 and 6677 is translated to 5677.

Next, you need to take the voice translation rule and assign it to a translation profile. The translation profile designates which the translation rule will change the caller (ID or ANI) or called (dialed number or DNIS) information. Example 6-23 assigns translation rule 1 to a translation profile called CHANGE_DID.

### Example 6-23 Assigning Translation Rules to a Translation Profile

```
HQ_RTR(config)# voice translation-profile ?
WORD Translation profile name
HQ_RTR(config)# voice translation-profile CHANGE_DID
HQ_RTR(cfg-translation-profile)# translate ?
called Translation rule for the calling-number
calling Translation rule for the calling-number
redirect-called Translation rule for the redirect-number
redirect-target Translation rule for the redirect-target
HQ_RTR(cfg-translation-profile)# translate called ?
<1-2147483647> Translation rule tag
HQ_RTR(cfg-translation-profile)# translate called 1
```

Example 6-23 assigns translation rule 1 as a called (dialed number) translation. Because the scenario requires you to change the ID information, this is the proper assignment. Assigning the translation rule as a calling translation would change the caller ID of a person calling into the organization.

The last step is to assign the translation profile. The following example assumes that the router is using POTS dial-peer 100 as inbound dial peer for calls coming from the PSTN:

```
HQ_RTR(config)# dial-peer voice 100 pots
HQ_RTR(cfg-dial-peer)# translation-profile incoming CHANGE_DID
```

Note that the example applies the translation profile in the incoming direction. This causes it to affect calls coming from the PSTN rather than outgoing calls. The translation profile is now in effect, accomplishing the objective of the scenario.

Note: You can do far more with translation profiles (and far more complex patterns that you can match with translation rules). This is covered more in the CVOICE exam of the CCNP Voice certification track.

Tip: If you are interested, I (Jeremy) recorded a free video that explains translation rules in depth. You can watch this video at www.cbtnuggets.com/series?id=440.

With all these various methods of digit manipulation, two questions quickly arise: Which method applied first? Will the router remove added prefix digits because of the automatic digit-stripping rule? Figure 6-16 answers these questions by displaying the order of operations for outgoing POTS dial peers.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_173_0.png)

Figure 6-16 Digit Manipulation Order of Operation for POTS Dial Peers

## Using CCP to Configure a CME Dial-Plan

If you prefer, you can also use the Cisco Configuration Professional (CCP) to modify the CME dial-plan. Cisco neatly organizes all dial-plan configurations in a Dial-Plans folder, shown in Figure 6-17.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_174_0.png)

6-17 Configuring a Dial-Plan Using CCP

Notice the first two items in the Dial-Plans folder of CCP are POTS and VoIP. These correlate to the two categories of dial peers you most frequently configure in CME. Selecting the POTS configuration item brings up the Create Dial-Plan menu. In an attempt to ease the configuration, Cisco provides three wizard-like configuration items:

- Create Incoming Dial-Plan: Allows you to configure inbound dial-peers using PSTN trunks.
- Create Outbound Dial-Plan: Allows you to configure outbound dial-peers using PSTN trunks. The wizard also provides you the ability to specify access digits (such as dialing 9 for an outline line) and caller ID information.
- Import Outgoing Dial-Plan Template: Allows you to import a dial-plan from a CSV template.

After you get comfortable with the CME configuration, you will likely access the Dial Peers tab (next to the Create Dial-Plans tab shown in Figure 6-17). In this configuration pane, you can manually create ten-configured dial peers through a GUI configuration. Figure 6-18 shows the creation of a ten-digit dialing dial peer.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_175_0.png)

**Figure 6-18** Configuring Dial Peers Using CCP

Unlike the POTS dial peer configuration window in CCP, the VoIP dial peer configuration does not have the wizard-based configuration items; it allows only the manual dial peer creation.

## Understanding and Implementing CME Class of Restriction

If you implement what you've seen so far, you can create a powerful VoIP system that supports both internal (IP) and external (dial peer) dialing. However, there might be times when you need to prevent some users from calling certain numbers, such as the following examples:

- Prevent standard employees from making international calls, but allow management to place international calls without restriction.
- Block certain high-cost numbers (such as 1-900 numbers in the United States)
- Prevent certain internal phones from reaching executive office directory numbers

This list goes on and on, but you get the idea: it's necessary to place calling restrictions on the VoIP network. If you were implementing this feature in the full CUCM, you would use Partitions and Search Spaces. In CME, the equivalent is called Class of Restriction (COR).
