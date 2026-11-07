```
b) if (x < 10) {
    if (y > 10)
        puts("*****");
    }
else {
    puts("#####");
    puts("$\$\$\$\$");
}
```

# 3.31 (Another Dangling-Else Problem)

Modify the following code to produce the output shown. Use proper indentation techniques. You may not make any changes other than inserting braces. The compiler ignores the indentation in a program. We eliminated the indentation from the following code to make the problem more challenging. [Note: It's possible that no modification is necessary.]

```
if (y == 8)
if (x == 5)
    puts("@@@@@");
else
    puts("#####");
    puts("$\$\$\$\$");
    puts("&&&&&");
```

a) Assuming x = 5 and y = 8, the following output is produced.

@@@@@
$\$\$\$\$
&&&&&

b) Assuming x = 5 and y = 8, the following output is produced.

@@@@@

c) Assuming x = 5 and y = 8, the following output is produced.

@@@@@
&&&&&

d) Assuming x = 5 and y = 7, the following output is produced.

#####
$\$\$\$\$
&&&&&

# 3.32 (Square of Asterisks)

Write a program that reads in the side of a square and then prints that square out of asterisks. Your program should work for squares of all side sizes between 1 and 20. For example, if your program reads a size of 4, it should print

****
****
****
****