```
STUDENT *ps;
```

which declares pointer ps to be a pointer to a student struct, we can dynamically create a student struct variable on the heap as follows:

```
ps = (STUDENT *) malloc(sizeof(struct student));
```

Note that we must cast the return value of malloc() to the appropriate type for pointer ps, which is STUDENT *, or a pointer to a student struct. We must also tell malloc() exactly how many bytes on the heap we want to allocate for this dynamic variable, in this case, sizeof(struct student) bytes.

We now have a pointer to a struct, ps. In order to access a field of the struct, we must first dereference the pointer (to get to the struct itself) and then use the direct component selector (.) operator to access the appropriate field of the struct.

For example:

```
*ps.age = 35;
```

Unfortunately, there's one problem here. The direct component selector (.) operator has precedence over the star (*) operator. Therefore, the above code will try to access a field of the struct before the pointer is dereferenced. Disaster always results from this!! The simple solution is to override precedence by using parenthesis:

```
(*ps).age = 35;
```

Now, the pointer to the struct is first dereferenced, giving us the struct itself, and then the appropriate field of the struct is accessed. Although this syntax is correct, C programmers almost never use it! The reason is that there is a shortcut syntax that requires less keystrokes and produces clearer code. The equivalent statement looks like this: