
## Display 11.16 Storing a SAS/IML module

```
libname mylib "C:\Users\baileraj.IT";      * location of catalog;
proc iml;

/* MODULE TO ESTIMATE PI
   - Monte Carlo integration used
   - Strategy:
       Generate X~Unif(0,1) and Y~Unif(0,1)
       Determine if Y <= sqrt(1-X*X)
       PI/4 estimated by proportion of times condition above is true
   - INPUT
       nsim = # simulations
       seed = seed for RANDGEN
   - OUTPUT
       estimate of PI along with SE and CI
*/

start MC_PI(nsim, seed);
    temp_mat = J(nsim,2,0);

    call randseed(seed);
    call randgen(temp_mat,'uniform');

    temp_mat=temp_mat||(temp_mat[,2]<=sqrt(J(nsim,1,1)-temp_mat[,1]##2));

    pi_over4 = temp_mat[+,3]/nsim;

    pi_est = 4*pi_over4;
    se_est = 4*sqrt(pi_over4*(1-pi_over4)/nsim);
    pi_LCL = pi_est - 2*se_est;
    pi_UCL = pi_est + 2*se_est;

    *------------------------------------------------------------;
    print 'Estimating PI using MC integration method with' nsim
          'data points';
    print pi_est se_est pi_LCL pi_UCL;

finish MC_PI;

reset storage=mylib.mystor;
store module= MC_PI;

quit;
```

Once this code is executed, an entry named MC_PI is included in the mystor catalog. The module can now be referenced with a two-level SAS name, and it can be loaded and used in future SAS sessions. Display 11.17 represents a future SAS session in which the MC_PI module is loaded and used.

## Display 11.17 Loading and using a SAS/IML module

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

## 11.9 Introducing SAS/IML Studio

SAS/IML Studio provides a highly flexible programming environment in which you can run SAS/STAT or SAS/IML analyses, and then display the results with dynamically linked graphics and data tables. In addition, SAS/IML Studio provides a way to call R functions from SAS (R Development Core Team, 2008). Earlier in this chapter, you learned that SAS/IML is a programming language for high-level, matrix-vector computations. IMLPlus is an extension of SAS/IML that contains additional programming features that enhance SAS/IML. IMLPlus is the language of SAS/IML Studio 3.2, a new statistical software product in SAS 9.2 intended for data analysts who write SAS programs to solve statistical problems, but who need more versatility for data exploration and model building.

IMLPlus enables techniques that are difficult or impossible to perform in SAS/IML, including calling SAS procedures without leaving SAS/IML, passing the value of a SAS/IML matrix directly to a SAS procedure, and creating and manipulating dynamically linked statistical graphics. Illustrations of many of the important features of SAS/IML Studio are provided in this section. However, a comprehensive review of these features is not. For more information, you can review the documentation for this product, which is available online at http://support.sas.com/documentation/onlinedoc/imlstudio/index.html. The SAS/IML Studio 3.2: User's Guide is extensive and provides a good tour of the GUI interface. SAS/IML Studio 3.2 for SAS/STAT Users might be a better and more concise starting point. This book provides numerous examples that create a basis for some of the examples in this section.

Before looking at examples, you should learn some basic vocabulary. The definition of *class* in the next paragraph and most of the information in this paragraph is excerpted from Chapter 1 of *SAS/IML Studio 3.2 for SAS/STAT Users*. SAS/IML Studio is a program that allows access to servers running SAS. You run SAS/IML Studio on a client computer, while the computer running SAS is the SAS server. These are often the same computer, but that isn’t required. It is important to understand where data reside and how to move it between the client and the server.

A key distinction between programming in SAS and programming in SAS/IML Studio is that SAS is a procedural programming language, and SAS/IML Studio is structured more like an object-oriented programming language. A *class* is defined as an “abstract package of data and functions that query, retrieve, or manipulate the data.” These functions are referred to as methods. An object is a particular instance of a class. Programmers coming to SAS from Java or C++ are excited to see this structure, whereas programmers from a FORTRAN or C background might find this a bit strange.

### 11.9.1 Case Study 1: Dynamic and interactive analysis of the SMSA data set

Chapter 6 included various static graphics showing the relationships between mortality and predictor variables in the SMSA data set.² In this case study, SMSA data tables are linked in SAS/IML Studio. In Display 11.18, a data table is constructed from importing the SMSA spreadsheet into SAS/IML Studio using menu options.

## Display 11.18 Creating linked data tables using File→Open→File

![](img/26474180ee55914c13fb9156a7678157_428_0.png)

Menus in the SAS/IML Studio interface enable additional analyses. In fact, you can use SAS/IML Studio as a menu-driven analysis tool. (For analysts with experience using SAS/INSIGHT, SAS IML Studio can be thought of as its successor with greater potential for extension and customization.) A scatter plot is generated using the **Graph** menu option, which opens the dialog box in Display 11.19. A character or numeric **Type** is associated with each variable in the data object. A measurement level of nominal (**Nom**) or interval (**Int**) is associated with each variable.

## Display 11.19 Options dialog box generated from selecting Graph→Scatter plot

![](img/26474180ee55914c13fb9156a7678157_429_0.png)

To produce a scatter plot of Mortality versus Education, left-mouse click Mortality and Set Y followed by a left-mouse click Education and Set X. This will produce a scatter plot like the one in Display 11.20. This scatter plot includes a regression line that is superimposed using the Fit Curves option. This option appears in a pop-up menu when you right-click in the scatter plot window. This menu enables you to change plotting symbols, symbol sizes, and other characteristics.

## Display 11.20 Superimposing a regression line using the Fit Curves option

![](img/26474180ee55914c13fb9156a7678157_429_1.png)

## 414 Statistical Programming in SAS

The real power of SAS/IML Studio is slightly revealed in Display 11.21. Points with high and low mortality relative to their peer cities with similar education levels are identified with a series of left-clicks. (In this context, a left-click is holding down the CTRL key and clicking on the point). This places the observation number on the plot and simultaneously highlights the observations in the data table. In particular, you can see that New Orleans, LA (observation 37) has the highest mortality rate and is usual among cities with similar education levels. San Jose, CA (observation 49) is noteworthy because the mortality rate is lowest among cities with high education levels.

## Display 11.21 Left-click selection of points linked to the data object

![](img/26474180ee55914c13fb9156a7678157_430_0.png)

You might want to select a collection of observations without separately clicking each point. Display 11.22 illustrates the use of a selection rectangle to highlight cities with average education levels of 12 or more. Try this at home: Right-click the χ² (second column of the data object) to the left of the city variable. Select Label by variable (pick city as the variable to use with labeling). Check out what happens when you select points now. If you are impatient, see Display 11.26 for the results.

## Display 11.22 Using a selection rectangle to select cities with highest average education levels

![](img/26474180ee55914c13fb9156a7678157_431_0.png)

### 11.9.2 Case Study 2: Multiple-linked graphics windows

The previous case study involved a single plot and a data object. You performed the actions using menu options or pointing and clicking. In this case study, it’s a bit more complicated. In particular, IMLPlus commands are used to read a previously constructed data set into SAS/IML Studio and create a permanent version of the SMSA data set. A scatter plot of MORTALITY versus EDUCATION is constructed. A histogram of January temperatures (JANTEMP) and a scatter plot of MORTALITY versus INCOME are constructed. Display 11.23 contains the declarations of these four objects (the data object, the histogram, and the two scatter plots). A method displays the data table containing the permanent version of the SMSA data. Methods display the histogram and two scatter plots. A method positions two of these plots.
