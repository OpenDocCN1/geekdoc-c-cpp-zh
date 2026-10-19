![](bbox=[0.12, 0.11, 0.22, 0.21])

Researchers at Hewlett-Packard, IBM, Hughes Aircraft, TRW, and other organizations have found that purging an error by the beginning of construction allows rework to be done 10 to 100 times less expensively than when it’s done in the last part of the process, during system test or after release (Fagan 1976; Humphrey, Snyder, and Willis 1991; Leffingwell 1997; Willis et al. 1998; Grady 1999; Shull et al. 2002; Boehm and Turner 2004).

In general, the principle is to find an error as close as possible to the time at which it was introduced. The longer the defect stays in the software food chain, the more damage it causes further down the chain. Since requirements are done first, requirements defects have the potential to be in the system longer and to be more expensive. Defects inserted into the software upstream also tend to have broader effects than those inserted further downstream. That also makes early defects more expensive.

![](bbox=[0.12, 0.35, 0.22, 0.45])

Table 3-1 shows the relative expense of fixing defects depending on when they’re introduced and when they’re found.

# Table 3-1 Average Cost of Fixing Defects Based on When They’re Introduced and Detected

| Time Introduced | Requirements | Architecture | Construction | System Test | Post-Release |
|---|---|---|---|---|---|
| Requirements | 1 | 3 | 5–10 | 10 | 10–100 |
| Architecture | — | 1 | 10 | 15 | 25–100 |
| Construction | — | — | 1 | 10 | 10–25 |

Source: Adapted from “Design and Code Inspections to Reduce Errors in Program Development” (Fagan 1976), Software Defect Removal (Dunn 1984), “Software Process Improvement at Hughes Aircraft” (Humphrey, Snyder, and Willis 1991), “Calculating the Return on Investment from More Effective Requirements Management” (Leffingwell 1997), “Hughes Aircraft’s Widespread Deployment of a Continuously Improving Software Process” (Willis et al. 1998), “An Economic Release Decision Model: Insights into Software Project Management” (Grady 1999), “What We Have Learned About Fighting Defects” (Shull et al. 2002), and Balancing Agility and Discipline: A Guide for the Perplexed (Boehm and Turner 2004).

The data in Table 3-1 shows that, for example, an architecture defect that costs $1000 to fix when the architecture is being created can cost $15,000 to fix during system test. Figure 3-1 illustrates the same phenomenon.