
| GET SOURCE CODE |
|---|
| DIR: c-programming |
| FILE(S): arguments.c |

For our example, we use an additional counter argc, to treat one argument after the other. This is useful in particular in case the program has additional options, see below. Here, the program arguments are treated via:¹⁴

```
int N;                 /* number of particles */
double temp;           /* temperature */
int argc = 1;          /* counter to treat arguments */

N = atoi(argv[argc++]);
sscanf(argv[argc++], "%lf", &temp);
```

Some simulation parameters are usually kept at their default values and they do not have to be passed as arguments each time. In this case, it is convenient to use program options to change the default values. Program options are usually indicated by a '-' character at the beginning, followed by some name, and maybe some additional values. A call to the example program including some options could look like

`arguments -size 10.3 -appendix XX 100 3.7`

Options and their accompanying values are stored in the argv[] strings like any other argument. Consequently, they can be processed using standard string manipulation. For instance, one can implement a loop, that is executed before the non-optional arguments are read, which is iterated as long as the "current" argument starts with a '-' character. Then, one can compare the "current" argument via strcmp to the different available options. If the option matches, one can take suitable actions, like setting a flag or assigning some parameter value. Finally, one should implement printing an error message in case the option passed as argument is not known to the program. For the example program, this could look like:

```
char appendix[1000];     /* to identify output file */
int do_save;             /* save files at end of output */
int print_help;          /* print help message ? */
double l;                /* lateral size of system */
int num_steps;           /* how many MD steps are performed */

/** default values **/
l = 10; do_save = 0; appendix[0] = 0;
```

14 For this program, no line numbers are given here because we discuss different parts of the example program in non-linear order.

First, if var is a variable of type ⟨type⟩, one can write

```
p = &var;
```

Now, as you know already from page 10, p contains the address where var is stored. Assigning a value to var will not change p. Nevertheless, one can access or change the content of var via *p.

The second possibility is that one acquires some available memory, and let p point to it. This works via the malloc() (“memory allocation”) function, which requires as argument the number of bytes to be allocated. It returns a pointer to “something” (i.e. of type void *), pointing to the reserved memory area:

```
void *malloc({size});
```

If the operating system cannot provide the requested memory, the special pointer value NULL is returned. Since the size of a type is determined using sizeof(), one can reserve a so far unused memory location where p can point to via:

```
p = ((type *) malloc(sizeof(type)));
```

Note the cast in front of the malloc() statement. This memory allocation does not take place during compile time or right when the program is started. It just happens, when the malloc() function is executed in the program. For this reason, the processes connected to malloc() are called dynamic memory management.

More interesting usages of pointers are possible. You could for instance have some init() function in your simulation (taking, say, an integer as argument) which also reserves some memory (where integers are stored) and returns the pointer to this memory. The function prototype might look like:

```
int *init(int);
```

On the other hand, functions can be referenced through pointers as well. To define a pointer fct_p, which points to a function taking an integer as argument and returning an integer, one writes

```
int (* fct_p)(int);
```

defined, while this is possible when using dynamic memory management. For this purpose, the `realloc()` function exists, which expects two arguments: 1. the pointer to the memory area to be extended and 2. the new size of the array:

```
void *realloc(〈pointer〉, 〈size〉);
```

The function returns a pointer to the new start of the memory chunk. This can be the same position as before the call. Nevertheless, it may sometimes be necessary to extend the memory chunk considerably. In this case it might happen that the operating system allocates a completely different part of the memory and copies the memory content from the old chunk to the beginning of the new chunk. In this case, the execution of the command might take some time, depending on the size of the memory area to be copied.

Note that one should pass only pointers to `realloc()` which have been allocated via `malloc()`, otherwise the behavior of the function is undefined. Also, it might happen that the available memory is not sufficient. In this case the special NULL pointer is returned.

If one wants to allocate a matrix dynamically, one has to do this in two steps. First, one has to allocate one array which will contain pointers to the beginning of each row, respectively. Now, within a loop, the memory areas for the different rows can be allocated. If `n_rows` and `n_cols` are the numbers of rows and columns, respectively, the code to allocate the matrix `mat` could look like

```
double **mat;
int n_rows = 10, n_cols = 10;
int i, j;

mat = (double **) malloc(n_rows*sizeof(double *));
for(i=0; i<n_rows; i++)
    mat[i] = (double *) malloc(n_cols*sizeof(double));
```

The access can be performed in the same way as for standard matrices; hence, one can write, e.g. to initialize all entries to 0:

```
for(i=0; i<n_rows; i++)
    for(j=0; j<n_cols; j++)
        mat[i][j] = 0;
```

Note that due to the way the dynamically allocated matrix mat is stored, the actual access is different from a standard matrix smat, which is defined via double smat[n_rows][n_cols]: A standard matrix is stored in one large chunk of memory, where each row follows the next. On the other hand, the different rows for the dynamically allocated matrix mat are usually stored in different places. Therefore, a direct access could look like *(*(mat+i)+j). This also means that a dynamically allocated matrix requires slightly more memory, because in addition to the actual matrix elements one needs an array with pointers storing the addresses of the different rows. Nevertheless, dynamically allocated matrices are more flexible, because the size can be changed during runtime. It is also possible that different rows contain a different number of elements, which is not possible for standard arrays either. This is useful, for example, when one wants to store an array of strings with strings of different lengths.

Finally, all memory which has been reserved inside the program should be released, one says freed again. For this purpose, the free() function can be used, which takes as argument a pointer to a previously allocated chunk of memory, e.g. like in:

```
free(p);
```

Freeing the memory which has been allocated for a matrix is performed in two steps: First, all rows are freed, then the array containing the pointers to the rows is freed. For the matrix mat this could look like:

```
for(i=0; i<n_rows; i++)
  free(mat[i]);
free(mat);
```

Freeing of memory is particularly important, if the memory is used only inside of some function and will not be accessed again after the execution of the function has terminated. If it is not freed, and if the function is called several times, then more and more memory is allocated during the execution of the program, which may cause the operating system to run out of memory. Such a bug is called a memory leak and should be avoided under all circumstances. A useful tool to detect memory leaks and other bugs connected with dynamic memory management is introduced in Sec. 4.3. These bugs are often hard to spot by hand.

Using dynamic memory management, arbitrarily complex data structures can be generated. More advanced examples like lists, trees, and graphs are discussed in Secs. 6.6 to 6.8.
