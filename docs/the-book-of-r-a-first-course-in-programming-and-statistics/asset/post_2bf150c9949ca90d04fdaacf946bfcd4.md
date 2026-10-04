
As a simple example of a while loop, consider the following code:

```r
myval <- 5
while(myval<10){
  myval <- myval+1
  cat("\nmyval' is now",myval,"\n")
  cat("\ncondition' is now",myval<10,"\n")
}
```

Here, you set a new object myval to 5. Then you start a while loop with the condition myval<10. Since this is TRUE to begin with, you enter the braced area. Inside the loop you increment myval by 1, print its current value, and print the logical value of the condition myval<10. The loop continues until the condition myval<10 is FALSE at the next evaluation. Execute the code chunk, and you see the following:

'myval' is 6
'condition' is now TRUE

'myval' is 7
'condition' is now TRUE

'myval' is 8
'condition' is now TRUE

'myval' is 9
'condition' is now TRUE

'myval' is 10
'condition' is now FALSE

As expected, the loop repeats until myval is set to 10, at which point myval<10 returns FALSE, causing the loop to exit because the initial condition is no longer TRUE.

In more complicated settings, it's often useful to set the condition to be a separate object so that you can modify it as necessary within the braced area. For the next example, you'll use a while loop to iterate through a vector and create an identity matrix (see Section 3.3.2) with the dimension matching the current integer. This loop should stop when it reaches a number in the vector that's greater than 5 or reaches the end of the integer vector.

In the editor, define some initial objects, followed by the loop itself.

```r
mylist <- list()
counter <- 1
mynumbers <- c(4,5,1,2,6,2,4,6,6,2)
mycondition <- numbers[counter]<=5
while(mycondition){
```

```r
mylist[[counter]] <- diag(mynumbers[counter])
counter <- counter+1
if(counter<=length(mynumbers)){
  mycondition <- mynumbers[counter]<5
} else {
  mycondition <- FALSE
}
n
```

The first object, mylist, will store all the matrices that the loop creates. You'll use the mynumbers to provide the matrix sizes, and you'll use counter and mycondition to control the loop.

The loopcondition, mycondition, is initially set to TRUE since the first element of mynumbers is less than or equal to 5. Inside the loop while, the first line uses double square brackets and the value of counter to dynamically create a new entry at position in mylist (you did this earlier with listed names in Section 5.1.5). This entry is assigned an identity matrix whose size matches the corresponding element of mynumbers. Next, the counter is incremented, and you now have to update mycondition. You want to check whether mynumbers[counter]<5, but you also need to check whether you've reached the end of the integer vector (otherwise, you can end up with an error by trying to retrieve an index position outside the range of mynumbers). So, you can use a statement to first check the condition<-mynumbers[counter]<5. If TRUE, then set mycondition to the outcome of mynumbers[counter]<5. If not, this means you've reached the end of mynumbers, so you make sure the loop exits by setting mycondition <- FALSE.

Execute the loop with those predefined objects, and it will produce the mylist object shown here:

# R mylist

```r
[[1]]
[,1] [2] [3] [4]
[1,] 1 0 0 0
[2,] 0 1 0 0
[3,] 0 0 1 0
[4,] 0 0 0 1
```

```r
[[2]]
[,1] [2] [3] [4] [5]
[1,] 1 0 0 0 0
[2,] 0 1 0 0 0
[3,] 0 0 1 0 0
[4,] 0 0 0 1 0
[5,] 0 0 0 0 1
```

```r
[[3]]
[,1]
[1,] 1
```

```r
[[4]]
| [1,] | 1 |
| [2,] | 1 |
```

As expected, you have a list with four members—identity matrices of size $4 \times 4, 5 \times 5, 1 \times 1$, and $2 \times 2$—matching the first four elements of mynumbers.
The loop stopped executing when it reached the fifth element of mynumbers (6) since that is greater than 5.

# Exercise 10.4

- a. Based on the most recent example of storing identity matrices in a list, determine what the resulting mylist would look like for each of the following possible mynumbers, without executing anything:
  - i. mynumbers <- (2,2,2,2,5,2)
  - ii. mynumbers <- 2:20
  - iii. mynumbers <- (10,1,10,1,2)

Then, confirm your answers in R (note you'll have to reset the initial values of mylist, counter, and mycondition each time).

- b. For this problem, I'll introduce the factorial. The factorial of a non-negative integer $x$, denoted as $x!$, refers to the product of all integers less than or equal to $x$. Formally, it is written like: $x! = x \times (x-1) \times \dots \times 1$.
