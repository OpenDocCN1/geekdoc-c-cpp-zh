This dummy function simply takes an ellipsis and converts it to a list with x <- list(...). This subsequently allows the object x to be treated the same as any other list. In this case, you can summarize the object by providing its names and class attribute. Here's a sample run:

```
R> unpackme(aa-matrix(1:4,2,2),bb=TRUE,cc=c("two","strings"),
d-factor(c(1,1,2,1))
Here is
in its entirety as a list:
$aa
[1] 1 [2]
[2] 2 4

$bb
[1] TRUE

$cc
[1] "two" "strings"

$dd
[1] 1 2 1
Levels: 1 2
```

The names of ... are: aa bb cc dd

The classes of ... are: matrix logical character factor

Four tagged arguments, aa, bb, cc, and dd, are provided as the contents of the ellipsis, and they are explicitly identified within unpackme by using the simple list(...) operation. This construction can be useful for identifying or extracting specific arguments supplied through ... in a given call.

| Exercise 11.2 |

a. Accruing compound interest is a common financial benefit for investors. Given a principal investment amount P, an interest rate per annum i (expressed as a percentage), and a frequency of interest paid per year t, the final amount F after years is given as follows:

```
F = P\left(1+\frac{i}{100t}\right)^{ty}
```