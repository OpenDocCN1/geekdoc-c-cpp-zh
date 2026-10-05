```
len = strlen(argv[1]);
for(i = 4; i < len; i++)
    if(argv[1][i] == ' ')
        break;
```

```
if(i == len)
{
    cout << "Second. is missing\n";
    return 0;
}
if((len-i-1) != 2 && (len-i-1) != 3)
{
    cout << "The last part should be two or three characters long\n";
    return 0;
}
cout << "The hostname " << argv[1] << " is valid\n";
return 0;
```

# FUNCTIONS WITH VARIABLE NUMBER OF PARAMETERS

A function may accept a variable number of parameters. One way of declaring such function, which comes from C, is first to put the fixed parameters, that is, those that must be present in the function, and then the symbol, known as ellipsis. In general, ... means “zero or more appearances of something”. For example the declaration:

```
void test(int num, char *str, ...);
```

indicates that test takes two fixed parameters, an integer and a pointer to a character, which may be followed by a variable number of additional parameters. In practice, you'll rarely need to write functions with a variable number of parameters. It might happen if you want to write a generic function, a function that accepts any number of values and returns their sum.

> A function that accepts a variable number of parameters must have at least one named parameter.

To call such a function, we first write the fixed arguments and then the values of the optional arguments. For example, we could call test() like this:

```
test(3, "example", 5, 8.9, "sample");
```

The data types of the optional arguments are int, float, char* with values 5, 8.9, and "sample", respectively.