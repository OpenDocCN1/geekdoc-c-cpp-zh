
descriptions of experimental conditions where each design was most appropriate.

These needs were satisfied by Cochran and Cox (1950)'s and Kempthorne (1952)'s books. However, Cochran and Cox and Kempthorne's books were published before the age of computers and they both emphasize extensive tables of designs, abundant formulas and numerical examples describing methods of manual analysis of experimental data and mathematical techniques for constructing certain types of designs. Since the publication of these books, use of experimental designs has gone far beyond agricultural research where it was initially employed, and a plethora of new books have been written on the subject. Even though computers and software (to both design and analyze data from experiments) are widely available, a high proportion of the more recent books on experimental design still follow the traditional pattern established by Cochran and Cox and Kempthorne by presenting extensive tables of designs and formulas for hand calculations and methods for constructing designs.

One of the objectives of this book is to break from the tradition and present computer code and output in place of voluminous formulas and tables. This will leave more room in the text to discuss the appropriateness of various design plans and ways to interpret and present results from experiments. The particular computer software illustrated in this book is SAS, which was originally developed in 1972. Its syntax is relatively stable and is widely used. SAS has probably the widest variety of general procedures for design of experiments and analysis of experimental data, including proc plan, proc factex, proc optex, and the menu driven SAS ADX for the design of experiments, and proc glm, proc varcomp, proc mixed and many other procedures for the analysis of experimental data. These procedures are available in the SAS/Stat and SAS/QC software.

### 1.9 Review of Important Concepts

This chapter describes the purpose for experimental designs. In order to determine if cause and effect relationships exist, an experimental design must be conducted. In an experimental design, the factors under study are purposefully varied and the result is observed. This is different from observational studies or sampling surveys where data is collected with no attempt to control the environment. In order to predict what will happen in the future, when the environment is controlled, you must rely on cause and effect relationships. Relationships obtained from observational studies or sampling surveys are not reliable for predicting future results when the environment is to be controlled.

Experimental designs were first developed in agricultural research, but are now used in all situations where the scientific method is applied. The basic definitions and terminology used in experimental design are given in this chapter along with a checklist for planning experiments. In practice there are many different types of experimental designs that can be used. Which design is used in a particular situation depends upon the research objectives and the experimental units. Figure 1.3 is a diagram that illustrates when the different experimental designs described in this book should be used. As different experimental designs are presented in chapters to follow, reference will be made back to this figure to when the designs should be used.

### Figure 1.3 Design Selection Roadmap

| | Estimate Variances | Study Factor Effects |
|---|---|---|
| **E.U.'s** | Homogeneous | Heterogeneous |
| **Block Factors** | One | Two |
| **Block size** | Large | Small |
| **Designs** | RCB, GCB | PBIB, BTIB, LSD |
| **One Factor** | RSE | CRD |
| **Multiple Factors** | class. cont. mixture | cont. class. |
| **Designs** | CRFD CRFF CRFD CRRS SLD SCD EVD RCFB BRS PCBf CCBF PBIB BTIB LSD BIB YSD | |
| **Multiple Factors with some hard to vary** | CRSP SPFF RSSP EESPRS SMPV RBSP | |

### 1.10 Exercises

- 1. A series of runs were performed to determine how the wash water temperature and the detergent concentration affect the bacterial count on the palms of subjects in a hand washing experiment.
  - (a) Identify the experimental unit.
  - (b) Identify the factors.
  - (c) Identify the response.

- 2. Explain the difference between an experimental unit and a sub-sample or sub-unit in relation to the experiments described in 1.

- 3. Explain the difference between a sub-sample and a duplicate in relation to the experiment described in 1.

- 4. Describe a situation within your realm of experience (your work, your hobby, or school) where you might like to predict the result of some future action. Explain how an experimental design, rather than an observational study might enhance your ability to make this prediction.

- 5. Kerry and Bland (1998) describe the analysis of cluster randomized studies where a group of subjects are randomized to the same treatment. For example, when women in some randomly selected districts are offered breast cancer screening while women in other districts are not offered the screening, or when some general practitioners are randomly assigned to receive one or more courses of special training and the others are not offered the training. The response (some characteristic of the patients) in the cluster trials must be measured on each patient rather than the group as a whole. What is the experimental unit in this type of study? How would you describe the individual measurements on patients?

## Completely Randomized Designs with One Factor

### 2.1 Introduction

In a completely randomized design, abbreviated as CRD, with one treatment factor, n experimental units are divided randomly into t groups. Each group is then subject to one of the unique levels or values of the treatment factor. If n = tr is a multiple of t, then each level of the factor will be applied to r unique experimental units, and there will be r replicates of each run with the same level of the treatment factor. If n is not a multiple of t, then there will be an unequal number of replicates of each factor level. All other known independent variables are held constant so that they will not bias the effects. This design should be used when there is only one factor under study and the experimental units are homogeneous.

For example, in an experiment to determine the effect of time to rise on the height of bread dough, one homogeneous batch of bread dough would be divided into n loaf pans with an equal amount of dough in each. The pans of dough would then be divided randomly into t groups. Each group would be allowed to rise for a unique time, and the height of the risen dough would be measured and recorded for each loaf. The treatment factor would be the rise time, the experimental unit would be an individual loaf of bread, and the response would be the measured height. Although other factors, such as temperature, are known to affect the height of the risen bread dough, they would be held constant and each loaf would be allowed to rise under the same conditions except for the differing rise times.

### 2.2 Replication and Randomization

Replication and randomization were popularized by Fisher. These are the first techniques that fall in the category of error control that was explained in Section 1.4.

The technique of replication dictates that r bread loaves are tested at each of the t rise times rather than a single loaf at each rise time. By having replicate experimental units in each level of the treatment factor, the variance of the experimental error can be calculated from the data, and this variance will be compared to the treatment effects. If the variability among the treatment means is not larger than the experimental error variance, the treatment differences are probably due to differences of the experimental units assigned to each treatment. Without replication it is impossible to tell if treatment differences are real or just a random manifestation of the particular experimental units used in the study. Sub-samples or duplicate measurements, described in Chapter 1, cannot substitute for replicates.

The random division of experimental units into groups is called randomization, and it is the procedure by which the validity of the experiment is guaranteed against biases caused by other lurking variables. In the bread rise experiment randomization would prevent lurking variables, such as variability in the yeast from loaf to loaf and trends in the measurement technique over time, from biasing the effect of the rise time.

When experimental units are randomized to treatment factor levels, an exact test of a hypothesis that the treatment effect is zero can be accomplished using a randomization test, and a test of parameters in the general linear model, normally used in the analysis of experimental data, is a good approximation to the randomization test.

A simple way of constructing a randomized data collection form, dividing n experimental units into t treatment groups, can be accomplished using the SAS data step commands. For example, in the bread rise experiment, if the experimenter wants to examine three different rise times (35 minutes, 40 minutes and 45 minutes) and test four replicate loaves of bread at each rise time, the following SAS commands will create the list.

```
/* The unrandomized design */
data unrand;
   do Loaf = 1 to 12;
      if (Loaf == 4) then time=35;
      if ( 5 <= Loaf <= 8 ) then time=40;
      if ( Loaf > 9 ) then time=45;
      dough_height=.;
      output;
   end;
run;
/* Sort by random numbers to randomize */
proc sort data=unrand out=crd; by u;
run;
/* Put Experimental units back in order */
data list;
   set crd;
run;
/* Print the randomized data collection form */
proc print double; var time dough_height; id Loaf;
run;
```

These commands create the levels of the factor (rise time) in order, create an additional column of random numbers using the ranuni() function, create the variable dough_height that contains a space to record the result in the output list, and then sorts the file by the random numbers to create a randomly ordered list. In the second data step the file crd is copied into a file called list, and the experimental units (loaves) are put back in sequential order. The proc print statement prints the SAS data file list using double spacing to allow room to write the response data after the experiments are run, and labels each
