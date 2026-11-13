```
{
    if(c==0)
        cout<<"subtraction of a,b"<<<a-b;
    else
        throw(c);
}
catch (int c)
{
    cout <<"Caught exception c="<<c;
}
```

# Output

Enter values of a,b:2 7
Exception caught:1
Enter values of a,b:7 4
Subtraction of a,b:3

In Program 1.28, a, b, c are integer variables. If a>=b then c gets a value 0 else it is 1. If c=0 subtraction of a,b is displayed. Otherwise, exception is caught.

# Multiple catch Statement: A try block can associate with more than one catch block; in such cases it may also have multiple throw statements.

```
try
{
    //try block
}
catch(argument)
{
    catch block 1
}
catch(arguments)
{
    catch block 2
}
.
.
.
.
.
.
.
catch(arguments)
{
    catch block n
}
```

When an exception is thrown, the compiler searches for the catch block that matches with the exception type thrown, then the catch block gets executed. If no match is found, the program terminates.

If the exception type matches with more than one catch block argument, then the first occurrence of catch that matches will be executed.