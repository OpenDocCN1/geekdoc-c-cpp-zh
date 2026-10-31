with one event occurring each time a payment is completed. This results in an event rate of 4,736 events per second over the four hours. These events always occur at periods of low claim submission activity. Thus, the normal peak rate, for analysis purposes, is 4,736 events/second.

Communication outages may result in additional peaks of activity (more analysis is warranted here). For the purposes of this analysis, we will consider that the capacity to process events at the expected peak rate of 4,736 events/second is adequate, with the full expectation that it will take time for the backlog of status reports to be cleared out. The assumption is that the EMS server will serve as a buffer for absorbing this backlog.

# Claim Status Timeout Rate

Noveau expects that 1% of claims will experience an issue resulting in a timeout event. Under normal conditions, the peak rate of these timeouts will follow the same pattern as the notification events, yielding a peak rate of 6.2 claims per second.

Outages, however, may result in significantly higher peak rates. If a communication outage prevents the delivery of notifications, the rate of timeouts may begin to approach the claim submission rate of 620 events/second.

# Claim Status Request Rate

Noveau is planning to make claim status information available to the members of its health care plans. It is anticipated that 1% of claims will result in claim status requests. This works out to 44,000 claim status requests per day. In lieu of better information, Nouveau is assuming that half of these requests will occur over four hours. This works out to about three requests per second.

From a performance perspective, this rate is so low compared to the status notification events that we will ignore them from a demand analysis perspective.

# Analysis

# Claim Processing

The component interaction pattern for monitoring claim processing is shown in Figure 15-13. Each step in the claim process results in a corresponding notification event. Six of the steps have associated SLAs