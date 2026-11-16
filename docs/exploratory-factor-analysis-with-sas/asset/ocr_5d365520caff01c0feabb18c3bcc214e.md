Guttman method. These methods are not very common and will not be discussed any further in the current chapter.

Each of the techniques described above are specified on the METHOD option in the FACTOR procedure. The different extraction methods summarized above can be requested using the following keywords.1

```
method =
PRINCIPAL /*PAF extraction*/
PRINIT /*Iterated PAF extraction*/
ALPHA /*Alpha extraction*/
ML /*ML extraction*/
ULS /*ULS extraction*/
IMAGE /*Image extraction*/
HARRIS /*Harris extraction*/
```

Please note, the PAF and iterated PAF techniques also require the PRIOR = SMC option (specifying use of the squared multiple correlation matrix for estimation of the initial communalities, as demonstrated in the sample syntax above). If this option is not specified, a PCA will be conducted.

# Three Pedagogical Examples

To illustrate the points in this section of the chapter, we have three example data sets that are available from the book website and will be used throughout the book. A quick summary of the data sets is presented in Table 2.1 on page 15. A complete summary of the items by instrument as well as source data source details are presented at the end of this chapter.

Table 2.1 Example data sets

| Example | Sample | Items/Scales | Example Items |
| :--- | :--- | :--- | :--- |
| 1. Engineering items | 372 undergraduate students from a study on engineering majors at an eastern university. | 14 items and 2 scales: engineering problem-solving (8 items), interest in engineering (6 items) | How well did you feel prepared for defining what the problem really is? Engineering fascinates me. |