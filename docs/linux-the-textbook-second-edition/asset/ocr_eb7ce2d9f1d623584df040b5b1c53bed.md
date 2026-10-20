|  | Before
movies | After
movies |
|---|---|
| movies[0]: | Silence of the Lambs | movies[0]: | Silence of the Lambs |
| movies[1]: | Malcolm X | movies[1]: | Malcolm X |
| ... | ... | ... | ... |
| movies[16]: |  | movies[16]: | Forest Gump |
| ... | ... | ... | ... |
| movies[65]: | The Birds | movies[65]: | Sleepless in Seattle |

FIGURE 13.1 The movies array before and after changing its contents.

```
$ echo ${#movies}
20
$ echo ${#movies[65]}
9
$ echo ${#movies[*]}
3
$ movies[16]="Forest Gump"
$ movies[65]="Sleepless in Seattle"
$ echo ${#movies[*]}
4
$ echo ${movies[0]}; echo ${movies[1]}; echo ${movies[16]}; echo ${movies[65]}
Silence of the Lambs
Malcolm X
Forest Gump
Sleepless in Seattle
$
```

It should be obvious by now that any shell variable that is assigned multiple values by using the assignment statement becomes an array variable. Thus, when a variable is assigned a multiword output of a command as a value, it becomes an array variable and contains each field of the output in a separate array slot. In the following example, files is an array variable whose elements are the names of all the files in the current directory. The numfiles variable contains the number of files in the current directory. The number of files can also be displayed using the echo ${#files[*]} command, as shown. The echo ${files[*]} command displays the names of all the files in the current directory, and the echo ${files[2]} command displays the third element (i.e., element at slot number 2).

```
$ files=`ls` numfiles=`ls | wc -w`
$ echo ${files[*]}
addall canleave countup debug_demo dext dext_functions diff2 exec.demo1 find_sys_const fs heredoc_demo trap_demo
$ echo $numfiles
12
$ echo ${#files[*]}
12
$ echo ${files[2]}
countup
$
```

In the following example, the num_array_demo file contains a script that uses an array of integers, called Fibonacci, computes the sum of integers in the array, and displays the sum on the screen. The Fibonacci array in this example contains the first ten numbers of the Fibonacci series. For those who are not familiar with the Fibonacci series, the first two numbers are 0 and 1, and the numbers are calculated by adding the previous two numbers. Mathematically, the series is represented as follows.

F₁ = 0