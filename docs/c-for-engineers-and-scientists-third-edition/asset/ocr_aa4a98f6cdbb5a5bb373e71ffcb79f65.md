Chapter 3 117
Formatting Numbers for Program Output

13. **(General Math)** Using Program 3.1, complete the following chart by determining the volume of cylinders having these radii and heights:

| Radius (in) | Height (in) | Volume |
|---|---||
| 1.62 | 6.23 | |
| 2.86 | 7.52 | |
| 4.26 | 8.95 | |
| 8.52 | 10.86 | |
| 12.29 | 15.35 | |

14. **(General Math)** The area of an ellipse (see Figure 3.5) is given by this formula:
$Area = \pi a b$ 

Using this formula, write a C++ program to calculate the area of an ellipse having a minor axis, $a$, of 2.5 inches and a major axis, $b$, of 6.4 inches.

![](bbox=[0.418, 0.403, 0.582, 0.463])

**Figure 3.5** The minor axis, $a$, and the major axis, $b$, of an ellipse

15. **(Modify)** Modify Program 3.1 to calculate the weight, in pounds, of the steel cylinder whose volume was determined in that program. This is the formula for determining the weight:
$weight = 0.28 (\pi)(r^2)h$

$r$ is the radius (in inches).
$h$ is the height (in inches) of the cylinder.

# 3.2 Formatting Numbers for Program Output

Besides displaying correct results, a program should present its results attractively. Most programs are judged on the perceived ease of data entry and the style and presentation of the output. For example, displaying a monetary result as 1.897 is not keeping with accepted report conventions. The display should be $1.90 or $1.89, depending on whether rounding or truncation is used.