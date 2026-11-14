# Figure 12.3 Illustration of Control Factors for Connector Experiment

![](bbox=[0.305, 0.11, 0.695, 0.305])

Therefore, this was not a split-plot experiment like the file example. The pointrep option of proc factex can be used to create a cartesian product design similar to the way it was shown in Section 8.2.1.

```
*Create noise factor design with factex;
proc factex;
factors F G;
output out=G1 nvals=(24 120) F nvals=(72 150) G nvals
=(25 75);
*Add the control factor design;
factors A B C D/nlevel=3;
model estimate=(A B C D);
output design=pointrep=s1 A cvals=('Low' 'Medium' 'High')
B cvals=('Thin' 'Medium' 'Thick')
C cvals=('Shallow' 'Medium' 'Deep')
D cvals=('Low' 'Medium' 'High');
proc print; run;
```

One of the comments that has been made about product array parameter design experiments popularized by Taguchi is that they require more experiments than are necessary. One of the main purposes of parameter design experiments is to detect interactions between control factors and noise factors. By understanding the interactions it may be possible to select levels of the control factors that will minimize the effect of the noise factors. By utilizing a cartesian product array design, all interactions between the factors in the control array and the factors in the noise array will be estimable. However, it may be possible to do this with fewer runs by utilizing resolution IV or resolution V fractional factorial designs where all interactions between control and noise factors are clear. Examples of this will be shown in Section 12.5.