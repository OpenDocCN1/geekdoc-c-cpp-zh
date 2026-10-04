Continuing with the current example, here's a Fibonacci function that stores the sequence in a vector and returns it:

```
myfib3 <- function(thresh){
  fibseq <- c(1,1)
  counter <- 2
  repeat{
    fibseq <- c(fibseq,fibseq[counter-1]+fibseq[counter])
    counter <- counter+1
    if(fibseq[counter]>thresh){
      break
    }
  }
  return(fibseq)
}
```

First you create the vector fibseq and assign the first two terms of the sequence. This vector will ultimately become the returnobject. You also create a counter initialized to 2 to keep track of the current position in fibseq. Then the function enters a repeat statement, which overwrites fibseq with c(fibseq[counter-1]+fibseq[counter]). That expression constructs a new fibseq by adding the sum of the most recent two to the contents of what is already stored in fibseq. For example, with counter at 2, the first run of this line will sum fibseq[1] and fibseq[2], appending the result as a third entry onto the original fibseq.

Next, the condition is checked. If the most recent value of fibseq[counter] is not greater than thresh, the loop repeats. If it is, the loop breaks, and returns the final line of myfib3. Calling returns the function and passes the specified returnobject (in this case, the final contents of fibseq).

After importing myfib3, consider the following code:

```
myfib3(150)
[1] 1 2 3 5 8 13 21 34 55 89 144 233
foo <- myfib3(10000)
foo
[1] 1 2 3 5 8 13 21 34 55 89 144
[13] 233 377 610 987 1597 2584 4181 6765 10946
bar <- foo[1:5]
bar
[1] 1 2 3 5
```

Here, the first line calls myfib3 with thresh assigned 150. The output is printed to the screen, but this isn't the result of the cat command as it was earlier; you can assign the returnobject to a variable, such as foo, and foo is now just another R object in the global environment that you can manipulate. For example, you could use it to create bar with a simple vector subset. This would not have been possible with either fib or myfib2.