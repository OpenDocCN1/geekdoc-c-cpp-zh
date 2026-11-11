# Discussion Questions

+   1. What is a pointer? How can it be initialized?

LO 13.1

LO 13.2

LO 13.2

+   2. Explain the effects of the following statements:

```
~~~
(a) int a, *b = &a;
(b) int p, *p;
(c) char *s;
(d) a = (float *) &x;
(e) double(*f)();
~~~
```

+   3. Distinguish between *(m)[5] and *m[5].

LO 13.5

LO 13.4

+   4. Given the following declarations:

```
~~~
int x = 10, y = 10;
int *p1 = &x, *p2 = &y;
~~~
```

What is the value of each of the following expressions?

```
~~~
(a) (*p1)++
(b) --(*p2)
(c) *p1 + (*p2)--
(d) ++(*p2) - *p1
~~~
```

+   5. Describe typical applications of pointers in developing programs.

LO 13.1

+   6. What are the arithmetic operators that are permitted on pointers?

LO 13.4

+   7. What is printed by the following program?

```
~~~
int m = 100;
int * p1 = &m;
int **p2 = &p1;
printf("%d", **p2);
~~~
```

LO 13.2

LO 13.3

+   8. Assuming name as an array of 15 character length, what is the difference between the following two expressions?
+       (a) name + 10; and
+       (b) *(name + 10).

LO 13.4

LO 13.5

+   9. What is the output of the following segment?

```
~~~
int m[2];
*(m+1) = 100;
*m = *(m+1);
printf("%d", m[0]);
~~~
```

LO 13.5

+   10. What is the output of the following code?

```
~~~
int m [2];
int *p = m;
m [0] = 100 ;
m [1] = 200 ;
printf("%d %d", ++*p, *p);
~~~
```

LO 13.4

LO 13.5