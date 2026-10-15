
class.) Finally, I was fortunate to receive a Barney Fellowship at Miami University, which provided some support to carve out time to work on material for this book.

No acknowledgments section would be complete without recognition of family. I am blessed with a family who is patient and supportive, even when I am distracted and cursing at a computer on a weekend afternoon when I could be doing other stuff. I would like to extend a big thank you to my kids–Sara, Jacob, Chris, and Emily–for the love, support, and joy that they bring into my life. Finally, I would like to acknowledge and thank my wife, Jenny. She is my best friend, a caring and constructive critic, an ardent supporter, and her love and support provide a wonderful foundation for attempting new projects. For the third time, I swear this is the last book that I will write.

## Part 1
## The Basics—Including Some Nuts and Bolts

+ Chapter 1 Let's Get Started—Preliminaries and a SAS Quick Start...... 3
+ Chapter 2 Reading, Combining, and Managing Data for Later Analysis ........................................ 23
+ Chapter 3 Using SAS Procedures ........................................................ 85
+ Chapter 4 Complex Table Construction and Output Control ........... 121
+ Chapter 5 Basic Models in SAS ..................................................... 155
+ Chapter 6 Producing Statistical Graphics in SAS ........................... 197
+ Chapter 7 Traditional SAS Graphics ............................................... 237

![](img/26474180ee55914c13fb9156a7678157_16_0.png)

## Let’s Get Started—
Preliminaries and a SAS Quick Start

1.1 Statistical Computing versus Programming versus Managing Data ......................................................... 4

1.2 Good Programming Practice ......................................................... 4

1.3 SAS Program Structure ......................................................... 9

1.4 What Is a SAS Data Set? ......................................................... 16

1.5 Internally Documenting SAS Programs ......................................................... 18

1.6 Summary ......................................................... 19

1.7 References ......................................................... 19

1.8 Exercises ......................................................... 19

Let’s begin with a working definition for statistical programming, and then follow with a description of the structure and appearance of a good statistical program. A short overview of the DATA step and procedures is presented with simple, but realistic examples. This provides a quick start for getting up and running with SAS programming.

![](img/26474180ee55914c13fb9156a7678157_18_0.png)

### 1.1 Statistical Computing versus Programming versus Managing Data

The computer is the analytic instrument and experimental tool for data analysts and statisticians. Analogous to chemists needing proficiency with mass spectrometers, and geneticists needing competence with gene and protein expression technologies, statisticians need skills using the computer as a tool for structuring data sets, conducting analyses, fitting models, and simulating stochastic systems. In the chapters that follow, I hope that you develop an appreciation for some of the questions that can be answered with statistical programming, and how these questions can be answered using SAS. The emphasis of this book is statistical programming. There is some consideration of managing data, and to a lesser degree, statistical computing. Statistical programming can be viewed as the coding required to conduct an analysis of interest, which might include using existing procedures or customizing an analysis not possible in existing procedures. In contrast, statistical computing might be considered the efficient coding of statistical procedures (e.g., numerical methods, random number generation, etc.). Data management might be conceptualized as the structure, storage, and manipulation of data files. This book is intended as an introduction that could lead you to more computational books, such as Givens and Hoeting (2005). These statistical programming ideas are introduced using SAS. There are a number of books that provide excellent introductions to SAS (e.g., Cody and Pass 1995, Delwiche and Slaughter 2008). I hope this book complements those other books by emphasizing the use of SAS to address statistical programming problems.

### 1.2 Good Programming Practice

I believe that good programming practice can go beyond "I know it when I see it." In this section, some guidelines for good practice are suggested. These guidelines are influenced by recommendations that I received in many programming classes over the years, and by regrets that I experienced when I looked at my own inadequately documented code years after it was constructed. As a final disclaimer, I usually follow these guidelines. However, in cases when I generate a quick program for a simple, single-use application, I might not follow these guidelines as closely. So, let’s start.

### Display 1.1 A SAS program that fits a multiple regression

```
/*      mreg-country-20may09.sas

Directory:  C:\baileraj\Classes\Spring09\programs\regression-examples
           [Laptop]
Author:     John Bailer
Purpose:    multiple regression example where average life expectancy
            of women is modeled as a function of country characteristics

Input data file - -------------------------------
            country.data

Directories:
            \\Casnov5\MST\MSTLab\Baileraj
            C:\Users\baileraj\BAILERAJ\Classes\Web-Classes\sta402\data

Input variables -------------------------------
Name = country name (Character variable)
Area = country area
Popsize = population size
Pcturban = % residents in urban setting
Lang = primary language
Liter = % literate
Lifemen = average life expectancy men
Lifewom = average life expectancy women
PcGNP = per capita gross national product

Created Variables -----------------------------
logarea = log10(area);
logpopn = log10(popsize);
loggnp = log10(pcGNP);
ienglish = (lang="English");

Data Source: Extracted from World Almanac
*/
* setting up macro variables for directories;
%let DIR1 = C:\Users\baileraj\BAILERAJ\Classes\Web-Classes\sta402\data;
%let DIR2 = \\Casnov5\MST\MSTLab\Baileraj;

data country;
title "country data analysis";
infile "&DIR1\country.data";

input name $ area popsize pcturban lang $ liter lifemen
      lifewom pcGNP;
logarea = log10(area);
logpopn = log10(popsize);
loggnp = log10(pcGNP);
ienglish = (lang="English");
drop area popsize pcgnp;
run;

proc print data=country;
run;

proc reg data=country;
    title "LITER and LOGGNP as predictors of Life expectancy of women";
    model lifewom = liter loggnp/ tol vif collinoint;
    output out=new p=yhat r=resid;
run;
```

### Display 1.1 *(continued)*

```
/* plot life expectancy of women vs. log(GNP) with a linear regression
   fit and LOESS fit superimposed
*/
ods rtf bodytitle
       title="C:\Users\bailera\Desktop\ch1-display-1_1-fig.rtf";
title "";
proc sgplot data=country;
  reg y=lifewom x=loggnp;
  loess y=lifewom x=loggnp;
run;
ods rtf close;
```

In the example, a block of comments is found at the beginning of this program (all text between the /* and */ symbols). The name of the program is the first line of the comment block. I use a convention where I build in the date as part of the filename. This is a habit that I find useful. The directory and author information follow in the next lines. I often use multiple machines, and it is helpful to identify this information here. Next, the purpose of the program is explained. After that, the name of the input data file is provided. The directories of the external data files and the input variables that they contain are identified next. The last two sections in the block describe other variables that are created and the original source of the data. The actual program statements follow. In this example, the comment block is longer than the program. While some people might think this is overkill, I have never regretted having too many comments, but I have regretted having too few. By the way, a second comment style was used in this code—a statement beginning with an asterisk and ending with a semicolon is a comment (in the code, see * setting up macro variables for directories;). A more useful version of this code might assign labels to variables in the data set. For example, the following statement would enhance the output of many statistical procedures:

```
label lenglish = "Indicator that English is primary language";
```

In addition, labels are attached to the variables in a SAS data set. This is discussed in more detail in upcoming chapters.

### 1.2.2 Use meaningful variable names

My first programming experience was with a version of FORTRAN that had an upper limit on variable names. You could use any variable name that included up to four characters. Variable names like B1 and X27 were common. Even SAS, earlier in its evolution, had a maximum of eight characters in variable names. Now, variable names can be up to 32 characters long and can include a mix of uppercase and lowercase letters and underscores. (This makes for easier reading of programs, although SAS is not case sensitive.) Variable names can begin with letters (a–z, A–Z) or an underscore (_ ) with
