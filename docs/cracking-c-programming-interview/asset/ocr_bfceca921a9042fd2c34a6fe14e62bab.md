Explanation: Structure 's1' is of 12B, 'a' is structure array. The indirection operator (->) x-> is equivalent to (*x).y.

| a[1] | | | | | | | |
||---|---|---|---|---|---|---||
| 2000 | 1 | 1012 | 3000 | 2 | 1024 | 4000 | 1000 |
| | 1000 | | | 1012 | | 1024 | | |
| Question-53 (i) | | | | | Question-53 (x) | | |
| | Naepur | Raipur | Kanpur | | | |
| | 2000 | 3000 | 4000 | | | |

```
Initialization:
struct s1 a[] = {"Naepur", 1, a+1}, "Raipur", 2, a+2}, "Kanpur", 3, a+3};
char *z;
struct s1 *ptr = a;
int;
struct s1 *p;
```

```
(i) a[0]->z -> 2000; //the content at this address gets printed by.
//Op: Nagpur
(ii) (*ptr)->z -> 2000.
//Op: Nagpur
(iii) ptr[1]->z is equivalent to (*ptr)->z; same as above.
(iv) a[2]->z -> (1024.p)->z -> 2000;
//Op: Nagpur
```

+   53. a

Explanation: Extension of the question.

```
(i) ((ptr->z) -> ++((1000),z) -> ++(2000) -> 2001; //at 2000 location character is there, step size is 12; //Op: aipur
(ii) a((ptr->z)->i)[z] -> a[1012.i,z]-a[2]->z -> 4000; //Op: Nagpur
//++ptr increased by 12, step size of struct is 12.
```

```
(iii) a-[(ptr->p)->i],z] -> a->((ptr->p)->i)[z] -> a[(*x)] -> a-(1024.p)->z -> a[-3]->z -> a[2]->z -> 4000; //Op: Kanpur
(iv) a[2],i -> *(a+2).i -> *(1024.i) -> -(2) -> 1;
//Op: 1
```

+   54. "etter" 'j' 9 "ancestor"

Explanation: A practice question.

+   55. c

Explanation: We already discussed these kinds of questions, explanation is not required.

+   56. b

Explanation: This program demonstrates a 1D array into a 2D array.