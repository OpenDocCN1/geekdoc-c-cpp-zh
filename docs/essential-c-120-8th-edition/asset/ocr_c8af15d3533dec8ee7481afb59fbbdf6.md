# Coding the Publish–Subscribe Pattern with Multicast Delegates

# Sequential Invocation

Figure 14.1 highlights the sequential notification of both heater and cooler.

![](bbox=[0.179, 0.175, 0.843, 0.506])

FIGURE 14.1: Delegate invocation sequence diagram

Although you coded only single call to OnTemperatureChange(), the call is broadcast to both subscribers. Thus, with one call, both cooler and heater are notified of the change in temperature. If you added more subscribers, they, too, would be notified by OnTemperatureChange().

Although a single call, OnTemperatureChange(), caused the notification of each subscriber, the subscribers are still called sequentially, not simultaneously, because they are all called on the same thread of execution.

# ADVANCED Delegate Internals

# Multicast Delegate Internals

To understand how events work, you need to revisit the first examination of the System.Delegate type internals. Recall that the delegate keyword is alias