# Data Variables and Constants

A computer, under the guidance of a program, can do many things. It can add numbers, sort names, command the obedience of a speaker or video screen, calculate cometary orbits, prepare a mailing list, dial phone numbers, draw stick figures, draw conclusions, or anything else your imagination can create. To do these tasks, the program needs to work with data, the numbers and characters that bear the information you use. Some types of data are preset before a program is used and keep their values unchanged throughout the life of the program. These are constants. Other types of data may change or be assigned values as the program runs; these are variables. In the sample program, weight is a variable and 14.5833 is a constant. What about 1700.0? True, the price of platinum isn’t a constant in real life, but this program treats it as a constant. The difference between a variable and a constant is that a variable can have its value assigned or changed while the program is running, and a constant can’t.

# Data: Data-Type Keywords

Beyond the distinction between variable and constant is the distinction between different types of data. Some types of data are numbers. Some are letters or, more generally, characters. The computer needs a way to identify and use these different kinds. C does this by recognizing several fundamental data types. If a datum is a constant, the compiler can usually tell its type just by the way it looks: 42 is an integer, and 42.100 is floating point. A variable, however, needs to have its type announced in a declaration statement. You’ll learn the details of declaring variables as you move along. First, though, take a look at the fundamental type keywords recognized by C. K&R C recognized seven keywords relating to types. The C90 standard added two to the list. The C99 standard adds yet another three (see Table 3.1).

# Table 3.1 C Data Keywords

| Original K&R Keywords | C90 K&R Keywords | C99 Keywords |
|---|---|---|
| int | signed | _Bool |
| long | void | _Complex |
| short |  | _Imaginary |
| unsigned |  |  |
| char |  |  |
| float |  |  |
| double |  |  |

The int keyword provides the basic class of integers used in C. The next three keywords (long, short, and unsigned) and the C90 addition signed are used to provide variations of the basic type, for example, unsigned short int and long long int. Next, the char keyword