```
```c
struct employee
{
int eno;
char ename;
float esal;
};
```
```

From the above, e.g., You can see that the key word struct is mandatory followed by the structure name and it opens braces for the members. The structure members here are the eno, ename, and esal and each of them are terminated with a semi colon and the closing braces for the structure is also terminated with a semicolon. Initializing the members Once the new structure data type has been declared, variables as per the programmers request can be defined of that type For example the structure variables e1,e2,e3 can be declared of the data type struct employee as depicted below:

```
```c
struct employee e1,e2,e3;
```
```

Now the question arises where do you declare the above statement, this can be done in the following different ways after the closing braces of the structures.

```
```c
};
/* closing brace*/

struct employee e1,e2,e3;
OR
} e1,e2,e3;
```
```

Once the declaring has been done you need to know if initializing can be done while declaring and the answer is positive. The format must be familiar to you, as it is similar to the one used in arrays. Take a look below at the format:

```
```c
struct employee
{
char ename[10];
float esal;
int eno;
};
struct employee e1 = {“ Johnny”, 500.00, 101};
```
```