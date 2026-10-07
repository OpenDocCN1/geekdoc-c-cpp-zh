# Chapter 4 Likelihood Models for Overdispersed Binomial Responses 105

The first link function in (4.35) assumes a common intra-litter correlation, i.e.,\n$\rho_\equiv(\rho)=\exp(\alpha_ho)/\{1+\exp(\alpha_ho)\}$. The other link function expresses the logs of the p's as\nof the main effects and its interaction (full model). Note that the overdispersed models\ndefined in (4.33), (4.34) and (4.35) fall all into the category of the Generalized\nOverdispersion Models previously defined in (4.31) and (4.32). We will now consider maximum\nlelihood estimation under the three distributions in (4.31) and (4.32) with three functions

```
$$\ln\left(\frac{\pi_{ip}}{1-\pi_{ip}}\right)=\beta_0+\beta,1(t=1)+\beta,1(p=1)-\beta,1(t=1,p=1)\n$\ln\left(\frac{\rho_{ip}}{1-\rho_{ip}}\right)=\alpha_0$(4.36)
```

4.4 contains the programming statements for fitting model (4.36) under the three\ndistributions in (4.33) using the NLMIXED procedure.

# 4.4: Fitting of Three Models to the Ossification Data Using NLMIXED

```
/*\nOssification Example from Morel and Neerchal (1997),\nStatistics in Medicine, 16, 2843-2853\n*/\ndata ossification;\nlength tx @@;\ninput tx @@ n @@;\ndo i=1 to n;\ninput t m @@;\nm = m - t;\noutput;\nend;\ndrop n;\nControl 8 8 10 9 9 7 0 0 5 3 3 5 9 10 5 8 5 1 6 0 5\nControl 16 7 8 9 7 10 10 6 6 1 9 8 6 7 5 5 7 9\n5 2 5 6 2 8 1 0 2 8 7 7 5\nPHT 1 9 9 1 4 3 7 4 0 7 0 4 8 1 7 2 2 8 1 7\n0 2 3 10 3 7 2 7 0 8 0 1 0 1 1\nTCPO 16 0 5 7 1 4 11 10 6 9 3 4 2 6 0 8 0 9\n5 6 2 9 7 3 1 0 8 8 6 9\nPHT+TCPO 11 2 2 0 1 8 7 1 0 0 4 0 6 0 7 6 6 6 1 6 7
```

```
ods html;ntitle "Binomial Distribution, Full Model on the Betas",\nproc mixed ossification;\nparms b0=0, b1=0, b2=0;\nif (tx=`Control')\nthen linp = b0;\nelse if (tx=`TCPO')\nthen linp = b0+b1;\nelse if (tx=`PHT')\nthen linp = b0+b2;\nelse if (tx=`PHT+TCPO')\nthen linp = b0+b1+b2+b3;\npi = 1/(1+exp(-linp));\nmodel t = -
```

Morel, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS. Copyright © 2017, SAS Institute Inc., Cary,
North Carolina, USA. ALL RIGHTS RESERVED. For additional resources, visit support.sas.com/support.