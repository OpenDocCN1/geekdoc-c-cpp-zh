required to maintain consistency. It is common to “instrument” these systems to detect data changes and update other systems.

This most common occurrence of this pattern involves reference data (customer, partner, product, etc.) that typically appears in many systems. This is also information for which inconsistencies may cause significant business problems. To minimize the inconsistencies and resolve them when they occur, the preferred approach to maintaining distributed reference data is to use the Master-Data-Management pattern.

# Master-Data-Management Pattern

The problem of minimizing, identifying, and reconciling inconsistencies among multiple sources is particularly important for reference data (e.g., information about customers, products, and partners). As the previous discussion of the Edit-Anywhere-Reconcile-Later pattern made clear, simply publishing the changes and having other systems subscribe to those changes and update their data cannot ever guarantee consistency and does nothing to resolve inconsistencies should they arise.

The Master-Data-Management pattern (Figure 12-5) is commonly employed to address this problem. The master data manager defines

![](bbox=[0.301, 0.603, 0.738, 0.858])

**Figure 12-5:** *Master-Data-Management Pattern*