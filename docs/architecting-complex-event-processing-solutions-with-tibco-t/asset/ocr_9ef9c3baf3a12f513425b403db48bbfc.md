triggering event. This makes the condition detector stateless, and therefore easy to scale and make highly available.

# Situation Recognition

The Situation Recognition pattern (Figure 3-7), on the surface, looks a lot like the Condition Detection pattern. However, there is a major difference: In the Situation Recognition pattern, the context data used to recognize a situation when the triggering event arrives contains historical information. Many of the triggering events that arrive do not result in a business event, but their occurrence results in the modification of the context data. The updated context data then provides the context for evaluating the next event that arrives.

Since the context data in this pattern contains historical information, the ability of the pattern to recognize a situation may be compromised if the historical data is lost. Such a loss would occur if the situation recognition component is holding context data in memory and the component is restarted. For this reason, the use of this pattern almost always requires persisting the historical information and recovering this information when the component restarts. The object persistence discussion in Chapter 6 discusses techniques for doing this.

There are many variations on this pattern both in the manner in which the context data keeps track of prior history and the manner in which the historical information is used to interpret a current event. Chapter 10 discusses a number of design patterns that can be used for this purpose.

![](bbox=[0.12, 0.82, 0.88, 0.94])

Figure 3-7: Situation Recognition Pattern