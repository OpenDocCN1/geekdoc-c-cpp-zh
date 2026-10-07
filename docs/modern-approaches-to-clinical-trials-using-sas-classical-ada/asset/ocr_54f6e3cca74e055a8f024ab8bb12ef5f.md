# Appendix D

Complete data are available in the supplemental materials.

Example Code 7.7 to Produce Results for Example 2

```
data neurodeg;
    input resp id dose time @@;
    datalines;
    191.70155 1 0 178.39954 1 0 3 167.33850 1 0
    6 149.50935 1 0 9 91.134853 1 0 12
\    205.09590 250 30 175.24421 250 30 3 152.41340 250 30
    6 113.48094 30 9 84.95754 250 30 12

    /* # of doses */
    proc sqlprint;
        select count(distinct(dose))format=1.0 into :n_dose from neurodeg;
    quit;

    /* initial model to obtain the matrix for calculation of the contrasts */
    ods output CoVB=(keep=col2-col6)
    ParameterEstimates=beta(where=(Effect ne "Intercept"));

    proc glimmix data=neurodeg;
        class dose id;
        model resp=dose*time/solution CoVB;
        random intercept time / type=UN subject=id;

    data omega;
        set omega;
        where effect ne "Intercept"
        drop effect;
    run;

    data models;
        length modnam $25;
        input modnam parl-3;
        datalines;
        emax 1.11
        quadratic -0.022 .
        exponential 8.867 . .
        linear . . .
    run;

    data doses;
        input dose @@;
        datalines;
        0 1 3 10 30
    run;

    /* calculate optimal contrast based on candidate models and and
```