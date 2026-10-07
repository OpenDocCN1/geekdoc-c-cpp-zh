Inset Statement: The INSET statement puts a box containing summary statistics in a graph associated with CDFFPLOT, HISTOGRAM, PPPLOT, PROPLOT, or QQQPLOT statements. Commonly used INSET options are listed in Table 9.14. For example, the code

HISTOGRAM AGE/NORMAL;
INSET MEAN STD ;

creates a plot with mean and standard deviation listed in an inset box within the graph frame.
For additional options see the SAS documentation.

# TABLE 9.14 Common OPTIONS for the PROC UNIVARIATE INSET Statement

| Option | Meaning |
|---|---|n| Display statistics | Indicates which statistics to report in the inset box. The list is the same as the statistics used in PROC MEANS. Commonly used statistics include NOBS, MEAN, STD, SUM, MIN, MAX, MEDIAN, and so on. For example.
PROC UNIVARIATE;
VAR AGE
HISTOGRAM AGE/NORMAL;
INSET STD MIN MAX | Allows you to specify labels and formats for displayed statistics. For example.
PROC UNIVARIATE;
VAR AGE
HISTOGRAM AGE/NORMAL;
INSET MEAN="Mean" (5.2) =St. Dev." (5.2); where the item in parentheses is a format applied to the displayed statistics |
| NORMALTEST | Displays a test for normality. To use, place a NORMALTEST option in the PROC UNIVARIATE statement and NORMALTEST and PNORMAL INSET option. For example.
PROC UNIVARIATE NORMALTEST;
VAR AGE;
HISTOGRAM AGE;
INSET PNORMAL; displays results of Shapiro-Wil test for normality |
| Inset position | Positions the inset box inside the graph frame using map-type specifications as NE (northeast upper right), NW, SE, SW (top middle), S (bottom middle). You may also position the box outside the frame using TM (top middle), BM, RM, or LM |
| Insert box title | Includes a title for the inset box by indicating it with a slash in the INSET statement using HEADER= FORMAT= and POSITION=. For example,
HISTOGRAM AGE;
INSET NORMAL/HEADER="Key Title"
POSITION=RM FORMAT=5.2; places the box frame at the right middle (RM) and formats all statistics using 5.2 |

NOFRAME Does not display a box around the inset
HEIGHT= Height of characters in the inset box. The default is 1