# ## 4.8.2 Analysis of a Latin Square Design

Latin square designs are frequently used in steer or dairy cow feeding experiments and in bioequivalence studies to compare different formulations of a drug in phase II clinical trials. In these studies the column blocking factor is time and the row blocking factor is animal or human subject. In some cases the treatment administered in one time period may have a carry-over effect on the response in the next period. However, if there is a sufficient washout period between column blocks, there will be no carry-over effects and the data can be analyzed as a traditional Latin square.

To illustrate the analysis of data from a Latin Square, consider the following bioequivalence study. The data is shown in Table 4.5 (taken from Selwyn and Hall, 1984).

Table 4.5 Treatment and Resulting AUC for Bioequivalence Study

| Subject | Period 1 | Period 2 | Period 3 |
| :--- | :--- | :--- | :--- |
| 1 | A 1186 | B 642 | C 1183 |
| 2 | B 984 | C 1135 | A 1305 |
| 3 | C 1426 | A 1540 | B 873 |

A=solution, B=tablet, C=capsule

The purpose was to test the bioequivalence of three formulations (A=solution, B=tablet, C=capsule) of a drug as measured by the AUC or area under the curve, which relates the concentration of the drug in the blood as a function of the time since dosing. Three volunteer subjects took each formulation in succession with a sufficient washout period between. After dosing, blood samples were obtained every half-hour for four hours and analyzed for drug concentration. AUC was calculated with the resulting data. Since there may be large variation in metabolism of the drug from subject to subject, subject was used as a row blocking factor. Since the absorption and metabolism of a drug will vary from time to time for a particular subject, time was used as a column blocking factor.

The SAS commands to read the data and fit model (4.9) and the resulting output are shown on the next page. The results indicate that there is no difference in the three formulations.