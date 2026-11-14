```
* Create 12-run Plackett-Burman Design in Data Step;
* first reads factor levels for first line from ;
* Table 6.9
* data li;
* input f1--f11;
* datalines;
1 -1 1 -1 -1 1 1 -1 1
1 -1 -1 -1 1 1 1 -1 1
* data pbl; set li;
* Next cyclically rotates factor levels;
array f(11) f1-f11;
array t(11) t1-t11;
do i=1 to 11;
  do j=1 to 11;
    if j<1 then k=11-i+1+j;
    else k=j-i+1;
    t(j)=f(k);
  end;
  output;
end;
do i=1 to 11;
  t(i)=-1;
end;
output;
keep t1-t11;
proc print; run;
```

As an example of the use of a Plackett-Burman design, consider the data in Table 6.11, which comes from a study by Hunter et al. (1982) of the fatigue life of weld-repaired castings. Seven factors were assigned to the last seven columns of the Plackett-Burman design matrix shown in Table 6.10, and the first four columns were not assigned to factors in defining the experiments. The purpose of the experiments was to identify the factors that affect the fatigue life of the weld repairs. The response, y, is the log of the lifetime of each weld repair. We will use this data to illustrate the analysis of data from a Plackett-Burman Design. Analysis of this data has been presented in the literature by several others.

Although there is no defining relation in a Plackett-Burman design, it is a resolution III design and the unsigned columns in Table 6.11 represent confounded strings of interactions. A first step in the analysis would be to calculate an effect for each of the 11 columns in Table 6.11 and make a half-normal plot.