but this time you stack statements by placing a new if declaration immediately following an else declaration:

```
if(a<=mynumber && mynumber>3){
cat("Same as 'first condition TRUE and second TRUE'")
a <- a2
b <- seq(1,a,length=mynumber)
} else if(a<=mynumber && mynumber<=3){
cat("Same as 'first condition TRUE and second FALSE")
a <- a2
b <- a*mynumber
} else if(mynumber>=4){
cat("Same as 'first condition FALSE and second FALSE")
a <- a-3.5
b <- a^(3-mynumber)
} else {
cat("Same as 'first condition FALSE and second FALSE")
a <- a-3.5
b <- rep(a+mynumber,times=3)
}
a
b
```

Just as before, only one of the four braced areas will end up being executed. Comparing to this version, to what was originally the first condition (a<=mynumber) being satisfied, but this time you use && to check two expressions at once. Neither of those situations is met, means the first condition is false, so in the third statement, you just have to check whether mynumber>=4. For the final else statement, you don't need to check any conditions because that statement will be executed only if all the previous conditions were not met.

If you reset a and mynumber to 3 and 4, respectively, and execute the stacked statements shown earlier, you get the following result:

```
Same as 'first condition TRUE and second TRUE'
R> a
[1] 9
R> b
[1] 1.000000 3.666667 6.333333 9.000000
```

This produces the same values for a and b as earlier. If you execute the code again using the second set of initial values (a as 6 and mynumber as 4), you get the following:

```
Same as 'first condition FALSE and second TRUE'
R> a
[1] 2.5
```