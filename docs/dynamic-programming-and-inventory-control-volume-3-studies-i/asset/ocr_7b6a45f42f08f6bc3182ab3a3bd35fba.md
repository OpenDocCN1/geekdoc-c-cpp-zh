We shall force a common cycle \( T \) for all products, so for instance we have the same number of orders \( \frac{1}{T} \) per year. This may not be optimal for a long period, but it simplifies the analysis considerably.

The production (order) of product \( j \) is \( q_j = T \lambda_j \). So we use \( T \) as the decision variable, and no more the level of orders. The EOQ formula for product \( j \) (expressed in \( T \)) leads to

\( C_j(T) = \frac{K_j}{T} + \frac{h_j}{2} \lambda_j T \left( 1 - \frac{\lambda_j}{r_j} \right),\)

and we must minimize \( \sum_j C_j(T) \).

# **Exercise 2.5.** Show that the optimal \( T = \hat{T} \) is

\( \hat{T} = \sqrt{\frac{2 \sum_j K_j}{\sum_j h_j \lambda_j \left( 1 - \frac{\lambda_j}{r_j} \right)}}.\)

# **2.6. LEAD TIME**

We have considered previously situations in which delivery is immediate, or is done at some rate per unit of time. The situation of Lead time is one when some delay is required to get the order (this delay is called the Lead Time). We will study the consequence of lead time on the EOQ model.

**2.6.1. NO SHORTAGE ADMITTED.** If \( L \) is the lead time, an order \( q \) will be delivered \( L \) units of time after the order is performed. If no shortage is admitted and if we do not perform any order during a lead time period then we must have the constraint

\( q \ge \lambda L,\)

otherwise we lose stock during a lead time period. After some time the stock will become negative which is not admitted. During a cycle (the period between two deliveries) of length \( \frac{q}{\lambda} \) the average cost is still

\( C(q) = K \frac{\lambda}{q} + \frac{hq}{2}.\)

The EOQ problem becomes

\( \min_{q \ge \lambda L} C(q).\)

In particular if \( \hat{q} \) defined by the EOQ formula satisfies the constraint, then it is the optimal value, whatever the value of \( L \) is. However, if the order is no more made when the inventory is 0 but when the inventory is \( \lambda L \). If \( \hat{q} \) does not satisfy the constraint, then the optimal order is simply \( \lambda L \), since by convexity \( C(q) \) will be increasing for \( q \ge \lambda L \). In this situation, one orders at time of delivery, and the stock at this time is also \( \lambda L \).

**2.6.2. POSSIBILITY OF BACKLOG.** We now describe an inventory model with lead time and the possibility of backlogging, see [41]. Backlog means that a negative inventory is possible. By negative inventory, one refers to the fact that the demand which cannot be met is recorded. It can be met later, but naturally there is a penalty in this case. The demand is continuous with a rate per unit of time \( \lambda \). The structure of cost is the following: there is a fixed ordering cost \( K \) and a variable ordering cost \( c \) (per unit of quantity ordered); a holding cost per unit of quantity \( h \), and a backlogging penalty per unit of quantity backlogged \( p \).