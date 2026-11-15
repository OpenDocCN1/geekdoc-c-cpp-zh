

| Character | Integer Equivalent | Binary Equivalent |
|---|---|---|
| ESC (Escape) | 27 | 0011011 |
| FS (File Separator) | 28 | 0011100 |
| GS (Group Separator) | 29 | 0011101 |
| RS (Record Separator) | 30 | 0011110 |
| US (Unit Separator) | 31 | 0011111 |
| SP (Space) | 32 | 0100000 |
| ! | 33 | 0100001 |
| " | 34 | 0100010 |
| # | 35 | 0100011 |
| $ | 36 | 0100100 |
| % | 37 | 0100101 |
| & | 38 | 0100110 |
| ' (Closing Single Quote) | 39 | 0100111 |
| ( | 40 | 0101000 |
| ) | 41 | 0101001 |
| * | 42 | 0101010 |
| + | 43 | 0101011 |
| , (Comma) | 44 | 0101100 |
| - (Hyphen) | 45 | 0101101 |
| . (Period) | 46 | 0101110 |
| / | 47 | 0101111 |
| 0 | 48 | 0110000 |
| 1 | 49 | 0110001 |
| 2 | 50 | 0110010 |
| 3 | 51 | 0110011 |
| 4 | 52 | 0110100 |
| 5 | 53 | 0110101 |
| 6 | 54 | 0110110 |
| 7 | 55 | 0110111 |
| 8 | 56 | 0111000 |
| 9 | 57 | 0111001 |
| : | 58 | 0111010 |
| ; | 59 | 0111011 |
| < | 60 | 0111100 |
| = | 61 | 0111101 |
| > | 62 | 0111110 |
| ? | 63 | 0111111 |
| @ | 64 | 1000000 |
| A | 65 | 1000001 |
| B | 66 | 1000010 |
| C | 67 | 1000011 |
| D | 68 | 1000100 |
| E | 69 | 1000101 |
| F | 70 | 1000110 |
| G | 71 | 1000111 |
| H | 72 | 1001000 |
| I | 73 | 1001001 |
| J | 74 | 1001010 |
| K | 75 | 1001011 |
| L | 76 | 1001100 |
| M | 77 | 1001101 |
| N | 78 | 1001110 |
| O | 79 | 1001111 |
| P | 80 | 1010000 |
| Q | 81 | 1010001 |
| R | 82 | 1010010 |
| S | 83 | 1010011 |
| T | 84 | 1010100 |
| U | 85 | 1010101 |
| V | 86 | 1010110 |
| W | 87 | 1010111 |
| X | 88 | 1011000 |
| Y | 89 | 1011001 |
| Z | 90 | 1011010 |
| [ | 91 | 1011011 |
| \ | 92 | 1011100 |
| ] | 93 | 1011101 |
| ^ (Circumflex) | 94 | 1011110 |
| _ (Underscore) | 95 | 1011111 |
| ` | 96 | 1100000 |
| ' (Opening Single Quote) | 97 | 1100001 |
| a | 97 | 1100001 |
| b | 98 | 1100010 |
| c | 99 | 1100011 |
| d | 100 | 1100100 |
| e | 101 | 1100101 |
| f | 102 | 1100110 |
| g | 103 | 1100111 |
| h | 104 | 1101000 |
| i | 105 | 1101001 |
| j | 106 | 1101010 |
| k | 107 | 1101011 |
| l | 108 | 1101100 |
| m | 109 | 1101101 |
| n | 110 | 1101110 |
| o | 111 | 1101111 |
| p | 112 | 1110000 |
| q | 113 | 1110001 |
| r | 114 | 1110010 |
| s | 115 | 1110011 |
| t | 116 | 1110100 |
| u | 117 | 1110101 |
| v | 118 | 1110110 |
| w | 119 | 1110111 |
| x | 120 | 1111000 |
| y | 121 | 1111001 |
| z | 122 | 1111010 |
| { | 123 | 1111011 |
| \| | 124 | 1111100 |
| } | 125 | 1111101 |
| ~ | 126 | 1111110 |
| DEL (Delete/Rubout) | 127 | 1111111 |

## APPENDIX C Using MATLAB to Plot Data from ASCII Files

To understand engineering problems and engineering solutions to problems, it is important to be able to visualize the numerical information that is involved. Therefore, the ability to easily obtain simple x-y plots from data files is an important capability in solving engineering problems.

In this appendix, we present a simple C++ program that generates a data file, and we then show how to use MATLAB to obtain a plot of the data. We chose MATLAB (MATrix LABoratory) to generate the plots in this appendix and also in the text chapters because it is an extremely powerful software environment for interactive numeric computations, data analysis, and graphics. An extensive discussion on generating different types of plots and on additional options that can be specified within the plots is included in Chapter 7 of _Engineering Problem Solving with MATLAB_, by D. M. Etter, Prentice Hall, 1993.

In the following example, we use a C++ program to generate an ASCII (American Standard Code for Information Interchange) data file, and we then plot the information using MATLAB. An ASCII data file can also be generated using a word processor, and then the same steps can be used to plot the information using MATLAB. If the data file is generated with a word processor, it is important to select the options for saving the file such that it is saved as a text file instead of as a word processor file.

The program that follows generates a data file containing 100 lines of information. Each line contains the corresponding time and function value from the equation for a damped sine function, namely,

$f(t) = e^{-t} \sin(2\pi t)$,

where $t = 0.0, 0.1, 0.2, \dots, 9.9$ seconds.

### C++ Program to Generate a Data File

```
/* -------------------------------------------------- */
/* Program app_c                                      */
/*                                                    */
/* This program generates a data file of values       */
/* from a damped sine function.                       */
/* -------------------------------------------------- */

#include<iostream>
#include <fstream>
#include <cmath>
using namespace std;
const double PI = 3.141593;

int main()
{
   /* Define objects.  */
   double t, f;
   ifstream dsin;

   /* Generate data file.  */
   dsin.open("dsine.dat");
   for (int k1=0; k1<100; k1++)
   {
      t = 0.1*(k1-1);
      f = exp(-t)*sin(2*PI*t);
      dsin << t << f << endl;
   }

   /* Close data file and exit program.  */
   dsin.close();
   return 0;
}
/*******************************/
```

### ASCII Data File Generated by the C++ Program

The data file generated by this program is an ASCII file that contains two numbers per line. The first few lines of information and the last line of information are

```
0.0   0.000
0.1   0.532
0.2   0.779
...
9.9   0.000
```

### Generating a Plot with MATLAB

To generate a plot of this information with MATLAB, we only need two statements. The first statement loads the file into the MATLAB workspace, and the second statement generates the xy-plot:

```
>>load dsine.dat
>>plot(dsine(:,1),dsine(:,2))
```

These steps generate the plot shown in Figure C.1.

Since it is important to label the information in a plot, we could also add the statements to give the plot a title, to label the axes, and to add a background grid:

```
>>load dsine.dat
>>plot(dsine(:,1),dsine(:,2)),
>>title('Damped Sine Function'),
>>xlabel('Time, s'), ylabel('f(t)'), grid
```

The plot with these labels is shown in Figure C.2.

![](img/0235a4ea835dc4575bd036e024a533b3_670_0.png)

Figure C.1 Plot of a damped sine function.

![](img/0235a4ea835dc4575bd036e024a533b3_670_1.png)

Figure C.2 Enhanced plot of a damped sine function.

## Appendix D References

- [1] “10 Outstanding Achievements, 1964–1989.” National Academy of Engineering, Washington, DC, 1989
- [2] Etter, D. M. Structured FORTRAN 77 for Engineers and Scientists, 4th ed. Benjamin/Cummings, Redwood City, CA, 1993.
- [3] “The Federal High Performance Computing Program: Executive Office of the President, Office of Science and Technology Policy,” Washington, DC, September 8, 1989.
- [4] Etter, D. M., and J. Bordogna. “Engineering Education for the 21st Century.” IEEE International Conference on Acoustics, Speech, and Signal Processing, April 1994.
- [5] Fairley, R. Software Engineering Concepts. McGraw-Hill, New York, 1985.
- [6] Etter, D. M. Engineering Problem Solving with MATLAB. Prentice Hall, Englewood Cliffs, NJ, 1993.
- [7] Plauger, P. J. The Standard C Library. Prentice Hall, Englewood Cliffs, NJ, 1992.
- [8] Jones, E. R., and R. L. Childers. Contemporary College Physics. Addison-Wesley, Reading, MA, 1990.
- [9] Etter, D. M. FORTRAN 77 with Numerical Methods for Engineers and Scientists. Benjamin/Cummings, Redwood City, CA, 1992.
- [10] Spanier, Jerome and Keith B. Oldham. An Atlas of Functions. Hemisphere Publishing Corporation, 1987.
- [11] Edwards, Jr., C. H., and D. E. Penney. Calculus and Analytic Geometry. 3d ed. Prentice Hall, Englewood Cliffs, NJ, 1990.
- [12] Master, G. M. Introduction to Environmental Engineering and Science. Prentice Hall, Englewood Cliffs, NJ, 1991.
- [13] Gille, J. C., and J. M. Russell, III. “The Limb Infrared Monitor of the Stratosphere: Experiment Description, Performance, and Results,” Journal of Geophysical Research, Vol. 89, No. D4, pp. 5125–5140, June 30, 1984.
- [14] Roberts, Richard A. An Introduction to Applied Probability. Addison-Wesley, Reading, MA, 1992.
- [15] Richardson, M. College Algebra, 3d ed. Prentice Hall, Englewood Cliffs, NJ, 1966.
- [16] Kahaner, D., Cleve Moler, and Stephen Nash. Numerical Methods and Software. Prentice Hall, Englewood Cliffs, NJ, 1989.
- [17] Ralston Anthony and Edwin D. Reilly, eds. Encyclopedia of Computer Science, 3d ed. Van Nostrand Reinhold Publishing Company, New York, NY, 1993.
- [18] Kreyszig, E. Advanced Engineering Mathematics. John Wiley & Sons, New York, 1979.
- [19] Wirth, Niklaus. Algorithms + Data Structures = Programs. Prentice Hall, Englewood Cliffs, NJ, 1976.
- [20] Stroustrup, Bjarne. C++ Programming Language. Addison Wesley, 1997.
- [21] Wampler, Bruce E. The Essence of Object Oriented Programming with Java and UML. Addison Wesley, 2002.
- [22] Kolman, Busby, Ross. Discrete Mathematical Structures. Prentice Hall, 2000.
- [23] www.wikipedia.com

