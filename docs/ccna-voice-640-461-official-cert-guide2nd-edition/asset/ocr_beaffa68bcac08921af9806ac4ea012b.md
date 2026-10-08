Note that the example applies the translation profile in the incoming direction. This causes it to affect calls coming from the PSTN rather than outgoing calls. The translation profile is now in effect, accomplishing the objective of the scenario.

Note: You can do far more with translation profiles (and far more complex patterns that you can match with translation rules). This is covered more in the CVOICE exam of the CCNP Voice certification track.

Tip: If you are interested, I (Jeremy) recorded a free video that explains translation rules in depth. You can watch this video at www.cbtnuggets.com/series?id=440.

With all these various methods of digit manipulation, two questions quickly arise: Which method applied first? Will the router remove added prefix digits because of the automatic digit-stripping rule? Figure 6-16 answers these questions by displaying the order of operations for outgoing POTS dial peers. The order remains the same for VoIP dial peers; however, most digit-manipulation commands apply only to POTS dial peers.

![](bbox=[0.148, 0.452, 0.853, 0.915])

Figure 6-16 Digit Manipulation Order of Operation for POTS Dial Peers