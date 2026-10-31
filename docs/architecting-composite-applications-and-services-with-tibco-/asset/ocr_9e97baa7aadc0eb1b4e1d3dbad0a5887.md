![](bbox=[0.1, 0.15, 0.9, 0.75])

Figure 11-14: Implementing Two-Tier Load Distribution Preserving Partial Ordering

For this pattern to work, there are a number of additional constraints that need to be followed. The service client must use a JMS transport, either XML over JMS or SOAP over JMS, to submit requests. The dispatcher must be in its own ActiveMatrix node and the JMS Binding Pool size on that node must be set to 1. The ActiveMatrix BusinessWorks processes must use the SOAP Event Source activity from the SOAP palette as the process starter and use the sequencing key of this activity.⁴

# Summary

When the volume of work exceeds the capacity of a single component, that work must be distributed among multiple workers. One common

4. If a sequencing key becomes available on the Service activity of the Service palette, it could be used in this pattern as well.