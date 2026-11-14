```
data powerRCB;
do b=2 to 5;
t=5;
nu=(t-1);
nu2=(b-1)*(t-1);
alpha=.05;
sigma=0.083487;
esize=.0460208;
Fcrit=finv(1-alpha,nu1,nu2);
ncb=<(css)/sigma2;
power=1-probf(Fcrit,nu1,nu2,nc);
output;
keep b nu2 nc power;
end;
proc print; run;
```

| Obs | b | nu2 | nc | power |
|---|---|---|---|---|
| 1 | 2 | 4 | 11.0247 | 0.32078 |
| 2 | 3 | 8 | 16.5370 | 0.68276 |
| 3 | 4 | 12 | 22.0493 | 0.89778 |
| 4 | 5 | 16 | 27.5617 | 0.96711 |

required for a CRD design to achieve adequate power for detecting a practical difference in means was r = 20, determined by the methods of Section 3.5.2. If blocking was expected to reduce the variance by 80% (i.e., \(\sigma^2_{rcb} = 0.20 \times \sigma^2_{crd}\), or \(RE = 5.0\)). Then the number of blocks required to achieve the same power with a RCB design is \(b = 20/5 = 4\).

# 4.6 Factorial Designs in Blocks

Blocking is even more effective when combined with a factorial design in treatment factors. In the case where more than one treatment factor is studied, the number of experimental units in each block must be equal to the product of levels of all the factors. This is called a randomized complete block factorial or RCBF. As an example of a blocked factorial experiment consider the data in Table 4.3. This experiment was conducted by Festing (2003) to determine whether BHA (a common antioxidant used in processed foods) induced activity of the liver enzyme EROD in mice and whether this activity was independent of strain of mice. It was part of a larger study to determine if antioxidants help protect against cancer.

The factors in this experiment are A, whether a mouse was treated with BHA or not, and B, the strain of the mouse. Since you can't assign a particular mouse to be of a certain strain, the experimental unit is not the mouse but the trial or conditions existing in the lab when a particular experiment was run. One run consisted of selecting a mouse from a specified strain; then either incorporating BHA in the diet (for a three-week period) or not (depending on