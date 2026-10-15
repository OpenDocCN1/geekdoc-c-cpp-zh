# Display 11.17 Loading and using a SAS/IML module

```
options nocenter;
libname mylib "C:\Users\baileraj.IT";    * location of catalog;
proc iml;
reset storage=mylib.mystor;
load module= MC PI;
run MC PI(2500,98765);
quit;
```

This code produces the estimate, standard error, and confidence limits.

```
pi_est   se_est   pi_LCL   pi_UCL
3.1792 0.0323078 3.1145844 3.2438156
```

# 11.9 Introducing SAS/IML Studio

SAS/IML Studio provides a highly flexible programming environment in which you can run SAS/STAT or SAS/IML analyses, and then display the results with dynamically linked graphics and data tables. In addition, SAS/IML Studio provides a way to call R functions from SAS (R Development Core Team, 2008). Earlier in this chapter, you learned that SAS/IML is a programming language for high-level, matrix-vector computations. IMLPlus is an extension of SAS/IML that contains additional programming features that enhance SAS/IML. IMLPlus is the language of SAS/IML Studio 3.2, a new statistical software product in SAS 9.2 intended for data analysts who write SAS programs to solve statistical problems, but who need more versatility for data exploration and model building.

IMLPlus enables techniques that are difficult or impossible to perform in SAS/IML, including calling SAS procedures without leaving SAS/IML, passing the value of a SAS/IML matrix directly to a SAS procedure, and creating and manipulating dynamically linked statistical graphics. Illustrations of many of the important features of SAS/IML Studio are provided in this section. However, a comprehensive review of these features is not. For more information, you can review the documentation for this product, which is available online at http://support.sas.com/documentation/onlinedoc/imlstudio/index.html. The SAS/IML Studio 3.2: User's Guide is extensive and provides a good tour of the GUI interface. SAS/IML Studio 3.2 for SAS/STAT Users might be a better and more concise starting point. This book provides numerous examples that create a basis for some of the examples in this section.