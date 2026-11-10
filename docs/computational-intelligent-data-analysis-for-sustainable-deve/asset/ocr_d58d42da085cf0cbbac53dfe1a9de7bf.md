# TABLE 6.1  Results of Multiple-Objective Linear Programming, Binary Linear Programming, and Benefit Targeting

|  | Multiple-Objective Linear Programming | Binary Linear Programming | Benefit Targeting |
|---|---:|---:|---:|
| Money spent | $1,924,423 | $2,027,195 | $1,934,422 |
| Environmental score | 5,736 | 6,613 | 4,208 |
| In-kind contributions | $640,170 | $603,641 | $424,141 |
| Number of projects funded | 100 | 119 | 59 |

# 6.2.1 Issue 1: How Best to Account for In-Kind Funding

On the surface, the amount of in-kind funding offered for a project is not significant because how the project is funded does not change the environmental benefit the project provides. However, the more in-kind funding a township offers, the fewer funds the county has to invest in a single project, thus allowing more projects to be funded. Townships do not necessarily have an incentive to offer large in-kind contributions, especially given constraints that limit the number of projects funded per applicant. As a result, an incentive must be established that maximizes the effectiveness of county funds spent by the program over time. The state does not require in-kind offers, so it is left to the counties to decide how to address such funding. The approach employed by Bradford County involves setting a minimum percentage of in-kind contribution and increasing the project’s environmental benefit score in the ranking process for every percentage point offered beyond the minimum. While it does insert in-kind contributions into the process, this ad hoc solution lacks flexibility and is not particularly elegant. As an alternative, we propose modestly restructuring the problem as a MOLP model.

As a MOLP model, instead of maximizing only environmental benefits, the algorithm would calculate both a maximum possible environmental benefit and a maximum in-kind funding offer, and the objective is to minimize weighted percentage deviations from the two maxima with 85% of the weight placed on environmental benefit and 15% on in-kind contributions. This 85:15 weighting scheme is arbitrary but was set as an initial estimation of weights with the purpose of emphasizing environmental benefit while still considering in-kind contribution levels. Other weights are explored later.”

¹ An interesting analysis would be to determine if there is an optimal weighting scheme that would maximize benefits over time. Unfortunately, such an analysis would require data on if and how townships reacted to changes in how in-kind contributions were treated in the decision process. This type of data is not currently available.