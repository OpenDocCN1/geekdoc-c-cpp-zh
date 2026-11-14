
```
data powerRCB;
do b=2 to 5;
t=5;
nu=(t-1);
nu2=(b-1)*(t-1);
alpha=.05;
sigma=0.083487;
esize=.0460208;
Fcrit=finv(1-alpha,nu,nu2);
nc=(css)/sigma**2;
power=1-probf(Fcrit,nu,nu2,nc);
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

## 4.6 Factorial Designs in Blocks

Blocking is even more effective when combined with a factorial design in treatment factors. In the case where more than one treatment factor is studied, the number of experimental units in each block must be equal to the product of levels of all the factors. This is called a randomized complete block factorial or RCBF. As an example of a blocked factorial experiment consider the data in Table 4.3. This experiment was conducted by Festing (2003) to determine whether BHA (a common antioxidant used in processed foods) induced activity of the liver enzyme EROD in mice and whether this activity was independent of strain of mice. It was part of a larger study to determine if antioxidants help protect against cancer.

The factors in this experiment are A, whether a mouse was treated with BHA or not, and B, the strain of the mouse. Since you can't assign a particular mouse to be of a certain strain, the experimental unit is not the mouse but the trial or conditions existing in the lab when a particular experiment was run. One run consisted of selecting a mouse from a specified strain; then either incorporating BHA in the diet (for a three-week period) or not (depending on what was specified); and finally humanely sacrificing the mouse and performing an autopsy to determine the activity level of the enzyme EROD in the liver. Since the results of in vivo experiments like this can vary substantially from time to time in the same laboratory due to differences in reagents used for the enzyme analysis, calibration of instruments, and environmental factors in the animal husbandry, the experiments were blocked in time. Two mice were selected from each of four strains, one was randomly chosen to receive BHA in the diet, and eight trials or runs were conducted simultaneously. This represented one block. Three months later, the whole process was repeated for a second block of runs. Since there are two levels of the treatment factor (BHA treated or control) and four levels of the factor strain, there were 2 × 4 = 8 experimental units or runs per block.

The model for analysis of a two-factor factorial in a randomized block design, like that shown in Table 4.3, is

y_{ijk} = μ + b_i + α_j + β_k + αβ_{jk} + ε_{ijk},  (4.7)

where b_i represents the block effect, α_j represents the treatment factor effect and β_k represents the strain factor effect. This model is easily generalized to multi-factor factorial designs in randomized blocks. Notice that in the model (4.7) there is an interaction αβ_{jk} between the two factorial factors, but there is no interaction between the block factor, b_i, and the factorial factors, α_j and β_k. The interactions with blocks are the error term for the analysis and if they are included in the model there will be zero degrees of freedom for sse.

The SAS commands to read this data and perform the analysis are shown on the next page with the resulting ANOVA table. There it can be seen that BHA treatment, strain, and the interaction are significant. The block sums of squares is also large resulting in a relative efficiency RE = 2.11. This means that it would take approximately three times as many mice to have the same power or sensitivity if the experiments were not blocked by time.

Figure 4.2 helps in interpreting the factorial effects and interaction. It can be seen that on the average, BHA added to the diet increases activity of the enzyme EROD in the mouse liver. However, this increase is nearly doubled for mice of strain BALB/c.

```
data bha;
input strain $ bha $ block erod;
datalines;
A/J Yes 1 18.7
A/J No 1 7.7
... etc.
proc glm; class strain bha block;
model erod=block bha strain bha*strain;
run;
```

| Source | DF | Sum of Squares | Mean Square | F Value | Pr > F |
|---|---|---|---|---|---|
| Model | 8 | 543.21750000 | 67.9021875 | 26.20 | 0.0002 |
| Error | 7 | 18.1400000 | 2.5914286 | | |
| Corrected Total | 15 | 561.3575000 | | | |
| Total | 15 | | | | |

| Source | DF | Type I SS | Mean Square | F Value | Pr > F |
|---|---|---|---|---|---|
| block | 1 | 47.6100000 | 47.6100000 | 18.37 | 0.0036 |
| bha | 1 | 422.3025000 | 422.3025000 | 162.96 | < .0001 |
| strain | 3 | 32.9625000 | 10.9875000 | 4.24 | 0.0527 |
| strain*bha | 3 | 40.3425000 | 13.4475000 | 5.19 | 0.0337 |

Figure 4.2 BHA Effect for Each Strain

![](img/878b651cdbe9da3d6d22e64d64b8a54f_141_0.png)

## 4.7 Generalized Complete Block Design

When experimental units represent physical entities, smaller groups or blocks of experimental units usually result in greater homogeneity. The larger the group, the more likely it is to have many experimental units that are widely different than the norm or average. For that reason it is unadvisable to have blocked designs with more than the minimum, t, experimental units per block, where t is the number of levels or combination of levels of treatment factors. However, in some cases where experimental units represent trials rather than physical entities and the experimental runs can be made quickly, larger block sizes may not increase the variability of experimental units within a block. In that case, a design with replicates of each treatment level within a block (called a generalized complete block design or GCB) can be used.

Consider the following example from Golf Magazine (Bastable, 2006, June). An experiment was conducted to determine the ideal tee height for driving a golf ball as far as possible. The purpose was to recommend to all readers of the article what tee height they should use. The treatment factor was the tee height as shown in Table 4.4.

Table 4.4 Treatment Factor Levels for Golf Experiment

| Level | Tee Height |
|---|---|
| 1 | Entire ball below crown |
| 2 | Half of ball above the crown |
| 3 | Bottom of ball at top of club-face |

An experiment consisted of a golfer hitting a golf ball from a specified height, and the response was the distance the ball traveled. To make a general conclusion, a representative group of golfers had to be used rather than one golfer. Since the ability to drive the ball by the golfers used in the study differed, it made sense to group or block the trials by golfer and randomize the order that each golfer hit a ball from each of the tee heights. However, since hitting more than three golf balls would not be likely to fatigue a golfer and cause more variability in his driving distance, there was no need to restrict a golfer to hitting just three balls. Instead, each golfer hit r = 5 golf balls from each of t = 3 tee heights. The results from this experiment are shown in the appendix. Nine golfers were used in this part of the study: each golfer hit five balls from each tee height (15 balls total) in a random order.

Since there are replicate experimental units for each treatment in each block, it is possible to fit the model

```
y_{ijk} = \mu + b_i + \tau_j + b\tau_{ij} + \epsilon_{ijk} (4.8)
```
