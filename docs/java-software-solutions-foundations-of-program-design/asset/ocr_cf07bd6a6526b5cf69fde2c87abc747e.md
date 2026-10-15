```
{
    int sum = 0;
    for (int num : list)
        sum += num;
    result = (double)sum / list.length;
}

return result;
}
```

Note the way the formal parameters are defined. The ellipsis (three periods in a row) indicates that the method accepts a variable number of parameters. In this case, the method accepts any number of int parameters, which it automatically puts into an array called list. In the method, we process the array normally.

We can now pass any number of int parameters to the average method, including none at all. That’s why we check to see if the length of the array is zero before we compute the average.

The type of the multiple parameters can be any primitive or object type. For example, the following method accepts and prints multiple Grade objects (we defined the Grade class earlier in this chapter):

```
public void printGrades (Grade ... grades)
{
    for (Grade letterGrade : grades)
        System.out.println (letterGrade);
}
```

A method that accepts a variable number of parameters can also accept other parameters. For example, the following method accepts an int, a String object, and then a variable number of double values that will be stored in an array called nums:

```
public void test (int count, String name, double ... nums)
{
    // whatever
}
```

The varying parameters must come last in the formal arguments. A single method cannot accept two sets of varying parameters.

Constructors can also be set up to accept a varying number of parameters. The program shown in Listing 8.11 creates two Family objects, passing a varying number of strings (representing the family member names) into the Family constructor.