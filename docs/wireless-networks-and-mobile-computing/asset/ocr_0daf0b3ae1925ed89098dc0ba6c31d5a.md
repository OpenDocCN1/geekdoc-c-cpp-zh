φ(y_i) satisfies the frequency separation requirement as specified by C with the previously assigned frequencies in this current phase at y_0, y_1, ···, y_{i−1}. Constraint (3.4) ensures that if φ(y_i) can be assigned at node y_i without any conflict with already assigned frequencies, the set of frequencies φ(y_i) + k × increment for k = 1, 2, 3, ···, can also be assigned at node y_i without any conflict. Note that for finding φ(y_0), we need to satisfy only Constraint (3.2). Constraints (3.3) and (3.4) are active for all other φ(y_i)’s where 0 < i ≤ m − 1.

```
**Algorithm Find_increment**

Y = (y_0, y_1, ···, y_{m−1})  
Q = (q_0, q_1, ···, q_{r−1})  
φ(Q) = (φ(q_0), φ(q_1), ···, φ(q_{r−1}))  
_origin_  
begin  
Set _increment_ = s_0;  
&nbsp;&nbsp;&nbsp;&nbsp;For i = 0 to m − 1 do  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;begin  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Find φ(y_i) as the least frequency in [_origin_, _origin_ + _increment_] which satisfies constraints (3.2), (3.3) and (3.4) as mentioned under Step 3.2.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If such φ(y_i) does not exist, set _increment_ = _increment_ + 1.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;end  
&nbsp;&nbsp;&nbsp;&nbsp;Return _increment_.  
end
```

**FIGURE 3.23:** Algorithm for finding increment

**Example 14.** _Consider X′ as shown in Table 3.16. The maximum demand in W is 45. Note that there is only one node in X′ (node 11) having the maximum demand in W. Hence, m = 1 and Y includes only the first node (node 11) in X′. The increment value obtained from **Find_Increment** (Y, Q, φ(Q), _origin_) is s_0 = 5 which is the initial value. In the subsequent phase of assignment, the demand vector will be modified and as a result, there may be multiple maximum demand nodes for which the increment value may be higher._

# **Step 4 (assign a single frequency):**