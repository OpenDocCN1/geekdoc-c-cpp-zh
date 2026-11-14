
However, the cookie-making process consists of the two steps as shown in Figure 8.1. Factor A was related to process step 1, while factors B and C were related to process step 2. The amount of shortening was a hard-to-vary factor because each time it was changed it required making a new batch of cookie dough, while the baking temperature and tray temperature were easy to vary. Once a batch of dough was made, there was enough to make six trays of cookies, and all six combinations of baking temperature and tray temperature could be tested within each dough batch, greatly reducing the total number of batches required.

Figure 8.1 Two-Step Cookie Making Process

![](img/878b651cdbe9da3d6d22e64d64b8a54f_317_0.png)

Therefore, an alternate way of designing the experiment would be to follow a two-step plan. First, plan to make four batches of cookie dough and randomly assign two batches to use 80% of the recipe recommended amount of shortening and two batches to receive the full amount of shortening recommended by the recipe. This represents a completely randomized design in one factor and the experimental unit is a batch of cookie dough. This first step is called the whole-plot design, and the whole-plot factor is A the amount of shortening. Next, bake six trays of cookies from each batch of dough and completely randomize the six combinations of bake temperature and tray temperature to the six trays of cookies within each batch. This is a randomized block 3 x 2 factorial within each batch of cookie dough and is called the sub-plot design. The sub-plot block is the batch of cookies, the sub-plot experimental unit is a tray of cookies and the sub-plot factors are B the bake temperature and C the tray temperature. The combination of the whole-plot and sub-plot design is called a split-plot design with CRD in the whole plots or CRSP.

By designing the experiment in this way only four plots of cookies are required instead of 12, and there are replicate whole-plot and sub-plot experimental units from which to estimate the variance of the two experimental error terms. There is less power for testing the shortening effect than there would be with the 12 batch completely randomized design shown in Table 8.1, but due to the blocking by batch, there is actually more power for detecting the baking temperature, tray temperature and interaction effects. For this reason split-plot experiments are often called super efficient.

## 8.2.1 Creating a Split-Plot Design with CRD in Whole Plots with SAS

proc factex that was described in Chapter 7 can be used to create a randomized plan for a split-plot experiment. The commands to do this are shown below.

```
*Create sub-plot design with factex;
proc factex;
    factors tray;
    output out=s1 tray=C vals=('Room' 'Hot');
run;
proc factex;
    factors bakeT /nlev=3;
    output out=s2 pointrep=s1 bakeT cvals=('low' 'norm' 'high');
run;
*Add the whole-plot design and randomize;
factex short;
    size design=4;
    output out=sp pointrep=s2 randomize(1012) short cvals=('80%', '100%');
run;
```

The first two sequences of the factors statement followed by an output statement create a file s2 that contains a full factorial in the three-level factor B and the two-level factor C in a sequential order with the levels of factor C changing fastest. The last sequence of the factors statement followed by an output statement creates a file sp that consists of a random ordering of the levels of the whole-plot factor A augmented by each line of the file s2 in a random order to create the split-plot design. The option randomize(seed) on the output statement creates the random ordering. Using the same seed will result in the same random ordering each time the code is run.

The commands below create a file of sequential batch and tray numbers within a batch and merge it with the randomized design created by proc factex.

```
data batches;
    do batch=1 to 4;
        do tray = 1 to 6;
            output;
        end;
    end;
run;
data sp;
    merge batches sp;
run;
proc print data=sp; run;
```

The resulting output appears on the next page. There it can be seen that batch 1 was randomly assigned to be made with 80% of the recipe-recommended shortening and the first tray of cookies from batch 1 was to be baked at the recipe-recommended temperature on a tray hot out of the oven, etc.

| Obs | batch | tray | short | bakeT | trayT |
|---|---|---|---|---|---|
| 1 | 1 | 1 | 100% | high | Hot |
| 2 | 1 | 2 | 100% | high | RoomT |
| 3 | 1 | 3 | 100% | norm | Hot |
| 4 | 1 | 4 | 100% | low | Hot |
| 5 | 1 | 5 | 100% | low | RoomT |
| 6 | 1 | 6 | 100% | norm | RoomT |
| 7 | 2 | 1 | 80% | low | RoomT |
| 8 | 2 | 2 | 80% | low | Hot |
| 9 | 2 | 3 | 80% | high | Hot |
| 10 | 2 | 4 | 80% | norm | RoomT |
| 11 | 2 | 5 | 80% | high | RoomT |
| 12 | 2 | 6 | 80% | norm | Hot |
| 13 | 3 | 1 | 80% | norm | Hot |
| 14 | 3 | 2 | 80% | low | RoomT |
| 15 | 3 | 3 | 80% | high | Hot |
| 16 | 3 | 4 | 80% | high | RoomT |
| 17 | 3 | 5 | 80% | low | Hot |
| 18 | 3 | 6 | 80% | norm | RoomT |
| 19 | 4 | 1 | 100% | norm | Hot |
| 20 | 4 | 2 | 100% | high | Hot |
| 21 | 4 | 3 | 100% | low | Hot |
| 22 | 4 | 4 | 100% | high | RoomT |
| 23 | 4 | 5 | 100% | low | RoomT |
| 24 | 4 | 6 | 100% | norm | RoomT |

In version 9.2 and later SAS proc factex has a uniteffect statement, that when used in conjunction with the blocks statement, can create split-plot designs with CRD in the whole plots as long as all the factors have the same number of levels. For example, in the cookie-baking experiment if only two levels of baking temperature were used rather than three, all factors would have two levels and the code below will create the split-plot design.

```
proc factex;
   factors shortening TrayTemp BakeTemp;
   size design=16;
   blocks units(batch=4);
   model estimate=(shortening|TrayTemp|BakeTemp);
   uniteffects batch / sub=(TrayTemp BakeTemp);
   output out=aptwo shortening cvals=('80%' '100%')
      TrayTemp cvals=('RoomT' 'Hot')
      BakeTemp cvals=('norm' 'high');
run;
proc print;
   var batch shortening TrayTemp BakeTemp;
run;
```

In this code proc factex uses the default of two levels on all factors since the nlevs option was left off the factors statement. The blocks statement specifies 4 levels of 'batch'. The uniteffects statement specifies batch as the whole-plot experimental unit. The option `whole = (Shortening) sub=(TrayTemp|BakeTemp)`; specifies that the factor Shortening will be aliased with differences in the whole-plot experimental units, and that TrayTemp, BakeTemp and their interaction will be sub-plot factors that are independent (or varied within levels) of the whole-plot experimental units.

## 8.2.2 Model for a Split-Plot Experiment with CRD in Whole Plots

It is easy to write the model for a split-plot design with a completely randomized design in the whole plots by following the same two-step procedure used to create the design. The first step was to create a completely randomized design in the whole plots by assigning the levels of the whole-plot factor at random to the whole plots. The model for this step can be represented as

```
$y_{ij} = \mu + \alpha_i + w_{(i)j}$ (8.1)
```

where \(y_{ij}\) represents the average response for the \(i\)th level of the whole-plot factor and the \(j\)th whole plot, \(\alpha_i\) represents the fixed effect of the whole-plot factor \(A\), \(w_{(i)j}\) represents the effect of the nested random effect of the \(j\)th whole plot assigned to the \(i\)th level of the whole-plot factor. This is the same model used for the completely randomized design in Chapter 2.

The second step in creating the design was to split the whole plots and assign each sub-plot at random to one of the levels of the sub-plot factor (or combination of levels of the sub-plot factors if there are more than one). Added to the model at this step is the effect of the sub-plot factor and the interaction between the whole-plot and sub-plot factor which are included after the random block term \(w_{(i)j}\) to arrive at the final model shown below

```
$y_{ijk} = \mu + \alpha_i + w_{(i)j} + \beta_k + \alpha\beta_{ik} + \varepsilon_{ijk}$ (8.2)
```

where \(y_{ijk}\) is the measured response for the \(i\)th level of the whole-plot factor and the \(k\)th level of the split-plot factor within the \(j\)th whole plot, \(\beta_k\) is the effect of the fixed split-plot factor, \(\alpha\beta_{ik}\) is the fixed interaction effect, and \(\varepsilon_{ijk}\) is the random effect of the \(k\)th split plot within the \(j\)th plot. If there are more than one sub-plot factors, as in the cookie-baking experiment described above, the model would be:

```
$y_{ijkl} = \mu + \alpha_i + w_{(i)j} + \beta_k + \gamma_l + \beta\gamma_{kl} + \alpha\beta_{ik} + \alpha\gamma_{il} + \alpha\beta\gamma_{ikl} + \varepsilon_{ijkl}$ (8.3)
```

and if there are more than one whole-plot factors the model would be written as:

```
$y_{ijklm} = \mu + \alpha_i + \beta_j + \alpha\beta_{ij} + w_{(ij)k} + \gamma_l + \alpha\gamma_{il} + \beta\gamma_{jl} + \alpha\beta\gamma_{ijl} + \varepsilon_{ijkl}$ (8.4)
```

and likewise for other combinations of numbers of whole-plot and sub-plot factors.
