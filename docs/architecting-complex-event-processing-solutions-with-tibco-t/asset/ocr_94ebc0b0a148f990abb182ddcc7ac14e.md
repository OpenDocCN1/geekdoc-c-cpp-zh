# Claim Tracker

The Claim Tracker is an example of a Track-and-Trace solution as described in Chapter 3. There are at least three processes associated with the Claim Tracker (Figure 15-5). The obvious process is Monitor Claim Processing—after all, that’s the whole point of the Claim Tracker. But monitoring doesn’t do any good if the resulting Claim Status is not made available to other participants. Thus a secondary process, Obtain Claim Status, is also required. However, even this is not enough. If the Claim Tracker determines that the process is not executing properly, it is best to proactively send a notification of the exception. This implies that there is yet a third process, Resolve Claim Processing Exception.

While it may be obvious that the Claim Tracker is responsible for Monitor Claim Processing and Obtain Claim Status, it should be equally obvious that the tracker is not going to resolve the problems leading to the exception. Figure 15-6 shows the configuration of the Claim Tracker, clarifying the communications channels and indicating that the exception-resolver role is being played by a person and some as-yet unspecified interface.

This design assumes that the claim processing participants are providing the requisite Claim Status Notifications. The next section will explore in more detail what notification is required and what information is retained in the Claim Status.

![](bbox=[0.165, 0.654, 0.839, 0.919])

**Figure 15-5:** *Claim Tracking Processes*