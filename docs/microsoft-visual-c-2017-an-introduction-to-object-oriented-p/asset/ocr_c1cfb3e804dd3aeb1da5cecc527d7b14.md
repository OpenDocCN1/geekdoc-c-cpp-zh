11. Which of the following catch blocks will catch any Exception object?

+   a. catch(Any e) { }
b. catch(Exception e) { }
c. catch(e) { }
d. All of the above will catch any Exception.

12. Which of the following is valid within a catch block with the header catch(Exception error)?

+   a. WriteLine(error.ToString());
b. WriteLine(error.Message);
c. return(error.ToString());
d. two of these

13. You can place statement(s) within a try.

+   a. zero
b. one
c. two
d. any number of

14. How many catch blocks must follow a try block within the same method?

+   a. only one
b. any number as long as it is greater than zero
c. any number as long as it is greater than one
d. any number, including zero or one

15. Consider the following try block. If x is 15, what is the value of a when this code completes?

```
try
{
    a = 99;
    if(x > 10)
        throw(new Exception());
    a = 0;
    ++a;
}
```

+   a. 0
d. undefined