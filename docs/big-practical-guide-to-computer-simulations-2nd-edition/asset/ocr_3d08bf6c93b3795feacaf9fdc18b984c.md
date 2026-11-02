next. Also, simulation programs need command line arguments, which are discussed afterwards. Finally, an easy method to compress data files during the simulation is presented.

The printf() ("print formatted") command consists of a format string and some (possibly zero) expressions to be evaluated and then printed:

```
printf( <format strings>, <argument 1>, <argument 2>, ...)
```

All arguments except the format string are optional. The format string may contain characters which are just printed as they are given. Furthermore, the format string determines how many of the optional arguments have to be given and it states how the values of these different arguments are to be printed. This is achieved using so-called conversion specifications, which are always preceded by the '%' character. Each conversion specification requires one argument, respectively. For example, a single integer is printed using %d, as shown in the following example:

```
int num_particles = 100;
```

```
printf("number of particles: %d\n", num_particles)
```

which will result in

```
number of particles: 100
```

This format string also contains a character \n, which is an escape sequence and means that the printing after this output has been printed will continue in the next line. The most important escape sequences are

|  |  |
|---|---|
| \n | a new line |
| \t | a horizontal tabulator |
| \b | a backspace |
| \\ | a backslash '\' |
| \" | a double quote " |

There are different types o conversion specifications. The most important ones, in the context of simulations, are