# Display 3.35 Randomization of four treatments to 20 experimental units (EUs) using PROC PLAN

generate randomization/allocation
assign: 4 treatments to 20 EUs

| Obs | _NAME_ | C1 | C2 | C3 | C4 | C5 | C6 | C7 | C8 | C9 | C10 | C11 | C12 | C13 | C14 | C15 | C16 | C17 | C18 | C19 | C20 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | EU | 3 | 6 | 12 | 8 | 9 | 7 | 13 | 4 | 18 | 1 | 19 | 17 | 20 | 15 | 10 | 16 | 5 | 14 | 11 | 2 |
| 2 | TRT | 1 | 1 | 1 | 1 | 1 | 2 | 2 | 2 | 2 | 2 | 3 | 3 | 3 | 3 | 3 | 3 | 3 | 3 | 3 | 3 |

# 3.13 Summary

The purpose of this chapter is to help you start working with SAS procedures. The chapter begins with a quick presentation of options that control the display of SAS output. The annotation of output using the TITLE and LABEL statements follows. The use of formats is introduced and illustrated. Data set properties are displayed using PROC CONTENTS. The values of variables in a data set are listed using the PRINT procedure. Basic statistical graphics are introduced (SGPLOT), with statistical summaries of categorical variables (FREQ) and numeric variables (MEANS, UNIVARIATE) following. The selection of a simple random sample (SURVEYSELECT) and the randomization of treatments to experiments units (PLAN) bring this chapter to its close.

# 3.14 References

Agresti, Alan. 2002. Categorical Data Analysis. 2d ed. Hoboken, NJ: Wiley Interscience.

Bailer, A. John, and James T. Oris. 1994. "Assessing toxicity pollutants in aquatic systems." Case Studies in Biometry. N. Lange, L. Ryan, L. Billard, D. Brillinger, L. Conquest, and J. Greenhouse, eds. New York, NY: John Wiley & Sons, Inc.

Cassell, David L. 2007. "Don't Be Loopy: Re-Sampling and Simulation the SAS Way." Proceedings of the SAS Global Forum 2007 Conference. Cary, NC: SAS Institute Inc. Available at http://www2.sas.com/proceedings/forum2007/183-2007.pdf.

Stokes, Maura E., Charles S. Davis, and Gary G. Koch. 2000. Categorical Data Analysis Using the SAS System. 2d ed. Cary, NC: SAS Institute Inc.