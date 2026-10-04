# 11.1.2 Using return

If there's no return statement inside a function, the function will end when the last line in the body has been run, at which point it will return the most recently assigned or created object in the function. If nothing is created, as in myfib and myfib2 from earlier, the function returns NULL. To demonstrate this point, enter the two dummy functions in the editor:

```
dummy1 <- function(){
aa <- 2.5
bb <- "string me along"
cc <- "string 'em up"
dd <- 4:8
}
```

```
dummy2 <- function(){
aa <- 2.5
bb <- "string me along"
cc <- "string 'em up"
dd <- 4:8
return(dd)
}
```

The first function, dummy1, simply assigns four different objects in its lexical environment (not the global environment) and doesn't explicitly return anything. On the other hand, dummy2 creates the same objects and explicitly returns the last one, dd. If you import and run the two functions, both provide the same return object.

```
R foo <- dummy1()
R foo
[1] 4 5 6 7 8
R bar <- dummy2()
R bar
[1] 4 5 6 7 8
```

A function will end as soon as it evaluates a return command, without executing any remaining code in the function body. To emphasize this, consider one more version of the dummy function:

```
dummy3 <- function(){
aa <- 2.5
bb <- "string me along"
return(aa)
cc <- "string 'em up"
dd <- 4:8
}
```