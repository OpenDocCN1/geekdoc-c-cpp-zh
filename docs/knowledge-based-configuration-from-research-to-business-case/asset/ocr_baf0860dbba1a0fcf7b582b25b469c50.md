**Table 13.6** Preferences of example user regarding mobile phone parameter values (obviously, price has the highest priority, i.e., should not be part of a diagnosis).

| r₀ : pStyle = clam | r₁ : pPrice < 70 | r₂ : pGPS = true |
|---:|---:|---:|
| 10 | 80 | 10 |

![](bbox=[0.365, 0.269, 0.637, 0.419])

**FIGURE 13.2**

Preferred diagnosis for inconsistent requirements ({r₀, r₁, r₂}): Δ₂.

conflicts: $CS_1 = \{r_0 : pStyle = clam, r_1 : pPrice < 70\}$ and $CS_2 = \{r_1 : pPrice < 70, r_2 : pGPS = true\}$. Both sets are conflict sets since $CS_1 \cup CK_B$ is inconsistent, and $CS_2 \cup CK_B$ is inconsistent as well. Furthermore, both conflict sets are minimal since no subset of these sets is a conflict set.

For each of the given minimal conflicts we have two possibilities to resolve the conflict. All the different alternative minimal diagnoses that can be determined from the given conflict sets are: $\Delta_1 = \{r_1 : pPrice < 70\}$ and $\Delta_2 = \{r_0 : pStyle = clam, r_2 : pGPS = true\}$. Thus, $\Delta_1$ and $\Delta_2$ indicate the possibilities a user has to adapt (or delete) his/her requirements in a way that the configuration system is able to identify a solution.

With some knowledge of the preferences of the user, we are able to rank the different alternative diagnoses and present the most relevant ones to the user. Since we have only two alternative diagnoses in our working example, we do not have to select the most relevant ones and only have to rank the two alternatives according to the preferences of the user. We determine the utility of a specific diagnosis $\Delta$ for a user with Formula 13.6. Let us assume that the preference values shown Table 13.6 were provided by a user.

$$utility(\Delta) = \frac{1}{\sum_{r \in \Delta} preference(r)} \tag{13.6}$$

The utility function in Formula 13.6 can be used within the diagnosis process (see also Felfernig et al., 2014). The hitting set directed acyclic graph for determining a personalized (preferred) diagnosis is depicted in Figure 13.2. In this context, $\Delta_2$ is the preferred diagnosis since it has the highest utility.