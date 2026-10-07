material for the book available from the companion website.

The input parameters in the %CRMSIM macro are listed below.

+   1. skeleton stores the prespecified skeleton (first column) and the true toxicity probabilities (second column).

+   2. target is the target toxicity rate.

+   3. cohort is the total number of cohorts.

+   4. cohortsize is the number of patients in each cohort.

+   5. toxstop is the threshold probability to early terminate the trial if the lowest dose level is too toxic.

+   6. ntrial is the number of replications in the simulation.

As an illustration, we consider the CRM with skeleton 1 under scenario 1 in Example Code 5.3 Simulation of CRM Design.

# Example Code 5.3 Simulation of CRM Design

```
data skeleton;
input p ptrue;
datalines;
0.02 0.07
0.08 0.12
0.12 0.17
0.20 0.30
0.30 0.45
0.50 0.60;
run;
%CRMSim(skeleton,target=0.3,ncohort=10,cohortsize=3,toxstop=0.9,ntrial=10000);
```

The output table includes the following variables.

+   1. doseselect is the percentage of each dose level being selected as the MTD.

+   2. ntox is the average number of DLTs observed at each dose level.

+   3. ntrted is the average number of patients assigned to each dose level.