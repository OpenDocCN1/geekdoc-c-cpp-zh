update reference data. Chapter 13 discusses this and other partitionings as well as the tradeoffs that need to be considered.

As should be obvious by now, there are many possible functional partitionings for CEP solutions. Some lead to simple and straightforward implementations. Others require clear architectural thinking to achieve the desired behavior in a robust and highly scalable fashion.

The following sections discuss a number of CEP solution design patterns, each focused on providing a commonly required business capability. For the most part, the patterns are arranged somewhat in order of increasing complexity. The chapter concludes with a brief discussion of problems for which there may not be a well-established design patterns.

For simplicity, the sensing component is not shown in these design patterns: It is assumed to be always present.

# Condition Detection

The simplest solution pattern you will encounter in complex-event processing is threshold detection (Figure 3-5). In this pattern, a component takes an action that can be observed and results in a technical event. The condition detector is listening for this event, whose arrival serves as the trigger for analysis. The analysis compares a value conveyed by the event to a threshold value and, if the event value exceeds the threshold value, generates a business event announcing this condition. Completing the pattern, another component is listening for these announcements and taking appropriate actions.

![](bbox=[0.15, 0.88, 0.9, 0.96])

Figure 3-5: Threshold Detection Pattern