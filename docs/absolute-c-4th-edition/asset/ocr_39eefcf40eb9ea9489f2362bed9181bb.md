# Display 10.3 Explanation of Display 10.2

```
int *p1, *p2;
```

```
p1 = new int;
```

```
*p1 = 42;
```

```
p2 = p1;
```

```
*p2 = 53;
```

```
p1 = new int;
```

```
*p1 = 88;
```

When the new operator is used to create a dynamic variable of a class type, a constructor for the class is invoked. If you do not specify which constructor to use, the default constructor is invoked. For example, the following invokes the default constructor:

```
SomeClass *classPtr;
classPtr = new SomeClass; //Calls default constructor.
```