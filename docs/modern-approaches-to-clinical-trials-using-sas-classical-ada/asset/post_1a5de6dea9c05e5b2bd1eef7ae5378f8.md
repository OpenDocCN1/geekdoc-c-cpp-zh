
![](img/f4ec2665c3484c528370923aeb5cb99f_275_0.png)

## 5.5 Time-to-Event Continual Reassessment Method

Using patients' exposure times as weights, Cheung and Chappell [12] proposed the time-to-event continual reassessment method (TITE-CRM) to incorporate information of follow-up into toxicity evaluation. Let $u_i$ be the actual follow-up time for subject $i$, and $y_i$ be the observed toxicity outcome at time $u_i$. If the $i$-th patient has not experienced the DLT, $y_i$ takes a value of 0, and $y_i=1$. Often a uniform weighting scheme is assumed in the form of $w_i=u_i/\tau$. The longer the follow-up, the higher the weight. The weight takes a value of 1 if the patient has experienced the DLT by time $u_i$. Under the CRM model, the pseudo-binomial likelihood function is given by

```
$L(\alpha|D) \propto \prod_{i=1}^{n} \{w_{i}p_{i(i)}^{\exp(\alpha)}\}^{y_{i}} \{1-w_{i}p_{i(i)}\}^{1-y_{i}}$
```

Under this formulation, patients who have not experienced toxicity and have not been fully followed are treated as "no toxicity" with $y_i=0$, although their data are in fact missing.

To illustrate the TITE-CRM, we consider a hypothetical trial that includes six dose levels. The target toxicity rate is 0.3, and the skeleton is specified as $(\rho_{1}, \dots, \rho_{6}) = (0.1, 0.2, 0.3, 0.4, 0.5, 0.6)$. In the trial, each patient is followed for 90 days, i.e., $\tau=90$. Suppose the entry date for the new patient is 20-April-2011. Before the entry of the new patient, nine patients have been treated, of whom the data are provided in Cumulative Data for the First Nine Patients in the TITE-CRM Trial.

Table 5.7 Cumulative Data for the First Nine Patients in the TITE-CRM Trial

| Patient | Dose Level | DLT | Follow-up | Date of Entry |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 1 | 0 | 0 | 01-Jan-11 |
| 2 | 1 | 0 | 0 | 02-Jan-11 |
| 3 | 1 | 0 | 0 | 15-Jan-11 |
| 4 | 2 | 0 | 1 | 01-Feb-11 |
| 5 | 2 | 0 | 1 | 05-Feb-11 |
| 6 | 2 | 1 | 2 | 20-Feb-11 |
| 7 | 3 | 1 | 3 | 03-Mar-11 |
| 8 | 3 | 0 | 3 | 07-Mar-11 |
| 9 | 3 | 0 | 3 | 10-Mar-11 |

The TITECRM macro (Example Code 5.5 Time-to-Event CRM Macro) implements TITE-CRM to determine the dose level for the new patient. The input variables are similar to those in the § fCRM.

## Example Code 5.5 Time-to-Event CRM Macro

```
currentdata;
  input doselevel DLT followup entry date7;
  datalines;
  1 0 0 01Jan
  1 0 0 02Jan
  1 0 0 15Jan
  2 0 1 05Feb
  2 0 1 20Feb
  2 1 1 03Mar
  3 0 1 07Mar
  3 0 1 10Mar
run;

data skeleton;
  input p;
  datalines;
  0.1
  0.2
  0.3
  0.4
  0.5
  0.6;
run;

%macro TITECRM(currentdata,skeleton,currenttime,tau=90,target=0.3,toxstop=0.9)
proc iml;
  use &skeleton;
  read all;
  use &currentdata;
  read all;
  currenttime=input(currenttime,'.date7');
  ndrow=row(p);
  doselevel={};
  dosecurr=doselevel(row(doselevel));
  w=(row+0)+(followup=1)%(currenttime-entrydate)/&tau;
  stop=0;

  start posterior (alpha) global (DLT,doselevel,p,w);
  sigma=2;
  lik=1;
```

```
nn=row(DLT);
aa=sum(DLT);

if aa==0 then
 do k=1 to nn;
 pi=?(p[doselevel[k]])##exp(alpha);
 lik=lik=((1-w[k]*pi)##(1-DLT[k]));
 end;
else
 do k=1 to nn;
 pi=?(p[doselevel[k]])##exp(alpha);
 lik=lik=((w[k]*pi)##(DLT[k]))*((1-w[k]*pi)##(1-DLT[k]));
 end;
end;

lik=exp(-0.5*alpha*alpha/sigma2);
return(lik);
finish;

/* used to calculate the posterior mean of pi */
start posttoxf(alpha) global(, DLT,doselevel,p);
post=p[j]##exp(alpha)*posterior(alpha);
return(post);
finish;

call qgrad("posterior", "posterior",.{M .P}) eps=1E-4 peak=-1
scale=0.5; /* default: PEAK=1 */
pi=();
 do j=1 to ndose;
 call quad(pj,"posttoxf",.{M .P}) eps=1E-4 peak=-1 scale=0.5;
 pj=pj/marginal;
 pi=pi/marginal;
 end;

lb=log(log(target)/log(p[1]));
call quad(poster,"posterior",-35|lb) eps=1E-4 peak=-1 scale=0.5;
postver=posttoxver/marginal;
 if postver>tostop then stop;
 diff-abs=abs(pi-target);
 dosebest=diff-abs)<c;
 if dosebest>dosecurr then
 if dosecurr<ndose then do
 dosenext=dosecurr+1;
 end;
 if dosebest<dosecurr then
 if dosecurr>1 then do
 dosenext=dosecurr-1;
 end;
 end;

if stop=1 then dosenext="The trial should be early terminated";
*title "dose for next patient"
 print dosenext;

doselevel=1:ndose;
doselevel=`doselevel\`;
 create doselevel from doselevel[colname="doselevel"];
 append from doselevel;

create pi from pi[colname="pi"];
 append from pi;
quit;

data &skeleton;
merge &skeleton. pi doselevel;
run;

*title "Skeleton Versus Estimated Toxicity";
proc sgplot data = skeleton;
line doselevel / response = p legend='p'
markeratrs=(symbol=circle) size=10) lineatrs=(pattern = solid);
line doselevel / response = p legend='pi'
markeratrs=(symbol=triangles) size=10) lineatrs=(pattern = solid);
yaxis min = 0 max = 1 label="Toxicity Probability";
xaxis label="Dose Level";
key location=inside lineatrs=(pattern = dash);
end;
%end TITECRM;

The posterior estimate of the toxicity rate is presented in Figure 5.5 Specified and Estimated Probabilities in the TITE-CRM, and the dose level to be assigned to the new patient is level 2.

![](img/f4ec2665c3484c528370923aeb5cb99f_279_0.png)

Based on an exposure-time weighting scheme, the weight function in the TITE-CRM may take various forms, among which the uniform weight is most straightforward. By contrast, the fractional CRM applies the Kaplan-Meier estimator to redistribute the censored data to the right, thus still yield an outcome between 0 and 1. Among all the DLTs that would occur in $(0, \tau)$, 70% of them are observed in $(\tau/2, \tau)$, the latter half of the assessment period. We take the sample size to be 36 patients and the skeleton as $(0.1,0.2,0.3,0.4,0.5)$. Under each scenario, 1000 trials are replicated. As shown in Scenario 1 of Study Comparing the fCRM and TITE-CRM and Scenario 2 of Study Comparing the fCRM and TITE-CRM, the results from fCRM and TITE-CRM are similar in terms of both the selection of the MTD and the number of patients treated at each dose. Similarly, TITE-CRM uses the same weight function for different levels, which takes into account the information. Due to the sparsity of the data, it would be difficult to accommodate levels in the Kaplan-Meier estimator or the weight function via stratification. Macros fCRM and TITECRM generate the results for Table 5.8 and Table 5.9 are also included in the supplemental material for the website. The location of the min.sas file should be specified in the %include statement in the fsim macro. The simulation is performed with fsim and TITECRM macros. The input variables for the two macros are:

- 1. skeleton is the data that includes the true toxicity rate and the skeleton.
- 2. target is the toxicity rate.
- 3. ncohort is the total number of cohorts.
- 4. cohortsize is the cohort size.
- 5. tau is the length of the follow-up period for evaluation of toxicity.
- 6. a is the length between recruitment times of adjacent cohorts.
- 7. stop is the threshold probability to early terminate the trial if the lowest dose level is too toxic.
- 8. trial is the number of replications.

As an example, Example Code 5.6 Simulation of fCRM and TITE-CRM generates the results for scenario 2 in Table 5.9; the output variables are the same as those in the sim.

## Example Code 5.6 Simulation of fCRM and TITE-CRM Designs

```
data skeleton;
input p ptrue;
datalines;
0.1 0.15
0.2 0.30
0.3 0.45
0.4 0.55
0.5 0.60
0.6 0.70;
run;
fCRMsim(skeleton,target=0.3,ncohort=12,tau=3,a=1,cohortize=3,
tostop=0.9,ntrial=1000);
TITECRMsim(skeleton,target=0.3,ncohort=12,tau=3,a=1,cohortize=3,
tostop=0.9,ntrial=1000);
```

Table 5.8 Scenario 1 of Study Comparing the fCRM and TITE-CRM

| Dose Level | 1 | 2 | 3 | 4 | 5 | 6 | # DLT | % Stop |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| P(Tox) | 0.04 | 0.08 | 0.12 | 0.20 | 0.30 | 0.50 | | |
| fCRM | 0 | 0.1 | 3.4 | 29.6 | 55.4 | 11.5 | | | |
| # Pts | 3.3 | 3.7 | 5.1 | 8.7 | 9.5 | 5.7 | 8.5 | 0 | |
| TITE-CRM | 0 | 0.1 | 3.5 | 30.9 | 53.9 | 11.6 | | | |
| # Pts | 3.4 | 3.7 | 5.2 | 8.5 | 9.5 | 5.6 | 8.5 | 0 | |

Table 5.9 Scenario 2 of Study Comparing the fCRM and TITE-CRM
