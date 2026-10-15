

## Display 6.22 (continued)

```
* Display 6.29: scatter plot paneled by constructed quartile variable;
proc sgpanel data=SMSA_from_txt;
  panelby JanTemp_quart;
  loess x=Education y=Mortality;
run;

ods rtf close;
```

The results of the various plots are presented in the following displays. The associated display produced by each SG procedure is noted as a comment in the code in Display 6.22. A histogram of the January temperatures with a superimposed density estimate is shown in Display 6.23. A right skew is clear, with most cities exhibiting January temperatures between 20 and 40 degrees Fahrenheit.

## Display 6.23 Histogram of January temperatures

![](img/26474180ee55914c13fb9156a7678157_242_0.png)

In Display 6.24, age-adjusted mortality appears to decline with an increase in education.

## Display 6.24 Scatter plot of mortality versus education

![](img/26474180ee55914c13fb9156a7678157_243_0.png)

It is interesting to investigate the relationship between one response variable and a collection of predictor variables. In Display 6.25, mortality is plotted versus education, income, and January temperature. It appears that mortality decreases with education and income, but does not vary with January temperatures.

## Display 6.25 Scatter plots with mortality on the y-axis for comparison

![](img/26474180ee55914c13fb9156a7678157_244_0.png)

You might expect education and income to be related, and you might want to examine their relationship with mortality and their relationship with each other. Display 6.26 shows the relationships and the distribution of each of the four variables.

## Display 6.26 Scatter plot matrix and histograms of mortality, education, income, and January temperature

![](img/26474180ee55914c13fb9156a7678157_245_0.png)

Conditioning a figure based on the levels of another variable is a cool way to explore relationships. In Display 6.27, the relationship between mortality and education is examined and is conditional on whether a city had average January temperatures of less than freezing.

## Display 6.27 Scatter plot of mortality versus education conditional on January temperatures

![](img/26474180ee55914c13fb9156a7678157_246_0.png)

An alternative to Display 6.27 is to plot both groups in the same figure, but use different plotting symbols and line types for fits. Display 6.28 uses PROC SGPLOT with a GROUP= option. This is opposed to PROC SGPANEL with a PANELBY= option, which was used to specify group differences in Display 6.27.

## Display 6.28 Scatter plot of mortality versus education conditional on January temperatures

![](img/26474180ee55914c13fb9156a7678157_247_0.png)

A scatter plot paneled by the quartiles of January temperatures is shown in Display 6.29. Display 6.29 emphasizes that the mortality and education relationship appears strongest in the cities with the warmest January temperatures. Do you want to suggest any explanations?

## Display 6.29 Scatter plot of mortality versus education paneled by quartiles of January temperatures

![](img/26474180ee55914c13fb9156a7678157_248_0.png)

## 6.7 Summary

The chapter began with a brief description of ODS Graphics. Customizing ODS Graphics using the ODS Graphics Editor and changing styles and templates were initially discussed. Next, the richness of SG procedures for data displays was explored.

There are many features and benefits of ODS Graphics that are not covered in this chapter. For a general introduction to ODS Graphics, see Chapter 21, “Statistical Graphics Using ODS,” in the SAS/STAT User’s Guide, Second Edition, and Rodriguez (2009) for a brief, high-level introduction to ODS Graphics. To customize your ODS Graphics to the extreme, learn more about GTL and its connection to ODS Graphics and the SGRENDER procedure.

## 6.8 References

Kuhfeld, Warren F. 2010. Statistical Graphics in SAS: An Introduction to the Graph Template Language and the Statistical Graphics Procedures. Cary, NC: SAS Institute Inc.

Kuhfeld, Warren F. 2009. “Modifying ODS Statistical Graphics Templates in SAS 9.2.” Proceedings of the SAS Global Forum 2009 Conference. Cary, NC: SAS Institute Inc. Available at http://support.sas.com/resources/papers/proceedings09/323-2009.pdf.

Lange, Nicholas, Louise Ryan, Lynne Billard, David Brillinger, Loveday Conquest, Joel Greenhouse, eds. 1994. Case Studies in Biometry. New Jersey: John Wiley & Sons, Inc.

Moore, David S., and George P. McCabe. 2003. Introduction to the Practice of Statistics. 4th Ed. New York, NY: W. H. Freeman and Co.

Robbins, Naomi B. 2005. Creating More Effective Graphs. Hoboken, NJ: Wiley-Interscience.

Rodriguez, Robert N. 2009. “Getting Started with ODS Statistical Graphics in SAS 9.2 (Revised 2009).” Cary, NC: SAS Institute Inc. Available at http://support.sas.com/rnd/app/papers/intods graph.pdf.

SAS Institute Inc. 2009. SAS/GRAPH 9.2: Reference. Cary, NC: SAS Institute Inc.

SAS Institute Inc. 2009. SAS/GRAPH 9.2: ODS Graphics Editor: User’s Guide. Cary, NC: SAS Institute Inc.

SAS Institute Inc. 2009. SAS/GRAPH 9.2: Graph Template Language Reference. Cary, NC: SAS Institute Inc.

SAS Institute Inc. 2009. SAS/GRAPH 9.2: Statistical Graphics Procedures Guide. Cary, NC: SAS Institute Inc.

Schwartz, Susan 2009. “Clinical Trial Reporting Using SAS/GRAPH SG Procedures.” Proceedings of the SAS Global Forum 2009 Conference. Cary, NC: SAS Institute Inc. Available at http://support.sas.com/resources/papers/proceedings09/174-2009.pdf.

Tufte, Edward R. 2001. The Visual Display of Quantitative Information. Second Edition. Cheshire, CT: Graphics Press.

## 6.9 Exercises

- 1. Refer to the packaging and log-bacterial growth data. Construct three different figures that display and summarize the data.
- 2. Refer to the nitrofen data. Generate a plot of the nitrofen data using the square root of TOTAL as the response variable versus concentration. Superimpose the fitted quadratic model. Only use PROC SGPLOT to generate this figure (i.e., don’t use PROC REG to generate fits first).
- 3. Refer to the nitrofen data. Fit a polynomial regression model (center the concentration variable). Use the ODS GRAPHICS statement to generate graphical summaries of this analysis.
- 4. Find a data set that interests you. Generate a display that best represents it using one of the SG procedures.

## Traditional SAS Graphics

- 7.1 Traditional SAS Graphics ............................................................ 238
- 7.2 Customizing Graphics ................................................................. 238
- 7.3 Why You Need to Learn about Annotate Data Sets .............................. 244
- 7.4 Case Study: Comparing Distributions of Responses ............................ 250
- 7.5 Descriptive Displays of Spatial Data ................................................. 254
- 7.6 Summary .................................................................................... 256
- 7.7 References ................................................................................. 257
- 7.8 Exercises .................................................................................... 257
- 7.9 Appendix: Complete Ohio County Population Data Set ......................... 258

![](img/26474180ee55914c13fb9156a7678157_252_0.png)

## 7.1 Traditional SAS Graphics

There are many traditional graphics procedures in SAS. These include procedures for producing scatter plots (GPLOT), three-dimensional plots (G3D), contour plots (GCONTOUR), charts (GCHART), and maps (GMAP). These procedures share features such as using the GOPTIONS statement for control and using annotate data sets for enhancements. In this chapter, the focus is on a few applications that highlight the benefits of traditional SAS graphics.

## 7.2 Customizing Graphics

When you invoke a graphics procedure, defaults for symbols, line types, axis tick marks, and labels are set. To see all of the defaults that are used, a scatter plot of the long-term relative frequency concept of probability is provided. In Display 7.1, 1200 virtual tosses of a fair digital coin are generated. A toss results in an OUTCOME=0 (tails) or OUTCOME=1 (heads). The number of heads (NUM HEADS) is accumulated and divided by the number of tosses (ITOSS) to define the relative frequency of heads (PROBABILITY HEADS). The relative frequency of heads is plotted versus the accumulated number of heads. For more information about the use of the RAND function with seeds set by STREAMINIT, see Section 8.11 or SAS Help.

## Display 7.1 Toss a digital coin–relative frequency of heads

```
data cointoss;
retain num_heads 0;
call streaminit(1234567);
do itoss = 1 to 1200;
  outcome = RAND('Bernoulli', 0.50);
  num_heads = num_heads + (outcome=1);
  probability_heads = num_heads / itoss;
  output;
end;
goptions reset=global;
ods rtf bodytitle file="C:\Users\baileraj.IT\Desktop\fig7p1.rtf";
proc gplot;
  plot probability_heads*itoss;
run;
ods rtf close;
```

The scatter plot is shown in Display 7.2.

