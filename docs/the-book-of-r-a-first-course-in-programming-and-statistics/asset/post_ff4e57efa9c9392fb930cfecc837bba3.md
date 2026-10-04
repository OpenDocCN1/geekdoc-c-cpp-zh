
As you've seen, a simple if statement won't work here. Since it accepts only a single logical value, it can't run through the entire logical vector produced by y=0.

```R
y=0
[1] FALSE FALSE FALSE FALSE TRUE FALSE FALSE FALSE FALSE FALSE
```

Instead, you can use the element-wise ifelse for this kind of scenario.

```R
R result <- ifelse(test=y==0,yes=NA,no=x/y)
R result
[1] -1.000000 -1.250000 -1.666667 -2.500000 -5.000000 NA 5.000000 2.500000
[9] 1.666667 1.250000 1.000000
```

Using exact matching, this command creates the desired result vector in one line. Three arguments must be specified: a logical-valued data structure, which provides the element to return if the condition is satisfied, and no gives the element to return if the condition is FALSE. As noted in the function documentation (which you can access with ?ifelse), the returned structure will be of "the same length and attributes as test."

## Exercise 10.1

a. Create the following two vectors:
`vec1 <- c(2,1,1,3,2,1,0)`
`vec2 <- c(3,8,2,2,0,0,0)`

Without executing them, determine which of the following if statements would result in the string being printed to the console. Then confirm your answers in R.

- i. if(vec1[1]==vec2[2]==10){cat("Print me!")}
- ii. if(vec1[1]==2&vec2[1]>2){cat("Print me!")}
- iii. if(all((vec2-vec1)[c(2,6)<7])){cat("Print me!")}
- iv. if(!is.na(vec2[3])){cat("Print me!")}

- b. Using vec1 and vec2 from (a), write and execute a code that multiplies the corresponding elements of the two vectors together if their sum is greater than 3. Otherwise, the code should simply sum the two elements.

- c. In the editor, write R code that takes a square character matrix and checks if any of the character strings on the diagonal (top left to bottom right) with the letter g or upper-case. If satisfied, these specific entries should be overwritten with the string "HERE". Otherwise, the entire matrix should be replaced with an identity matrix of the same dimensions. Then, try your code on the following matrices, `as.character(1:16),4,4`

- i. `ymat <- matrix(c("DANDELION", "Hyacinthus", "Gerbera"`
- ii. `ymat <- matrix(c("MARIGOLD", "geranium", "ligularia", "Pachysandra", "SNAPDRAGON", "GLADIOLUS"),3,3)`
- iii. `ymat <- matrix(c("GREAT", "exercises", "right", "here"),2,2,rowby=T)`

Hint: This requires some thought—you will find the function from Section 3.2.1 and substr from Section 4.2.4 useful.

## 10.1.4 Nesting and Stacking Statements

If an statement can itself be placed within the outcome of another statement, by nesting or stacking statements, you can weave intricate paths of decision-making by checking a number of conditions at various stages during execution.

In the editor, modify the mynumber example once more as follows:

```R
if(a<mynumber){
cat("First condition was TRUE\n")
a <- "a2"
if(mynumber>3){
cat("Second condition was TRUE\n")
b <- seq(1,a,length=mynumber)
} else {
cat("Second condition was FALSE\n")
b <- a-mynumber
}
} else {
cat("First condition was FALSE\n")
a <- a-3.5
if(mynumber>4){
cat("Second condition was TRUE\n")
b <- a*(3-mynumber)
} else {
cat("Second condition was FALSE\n")
b <- rep(a+mynumber,times=3)
}
a
b
```

You you here the same initial decision being made earlier. The value a is squared if it's less than or equal to mynumber; if not, it has 3.5 subtracted from it. But now there's another if statement within each braced area. If the first condition is satisfied and a is squared, you then check whether mynumber is greater than 3. If TRUE, b is assigned seq(1,a,length=mynumber). If FALSE, b is assigned a+mynumber.

If the first condition fails and you subtract 3.5 from a, then you check whether mynumber is greater than or equal to 4. If it is, b becomes a*(3-mynumber). If it's not, b becomes rep(a+mynumber,times=3). Note that I intend the code within each subsequent braced area to make it easier to see which lines are relevant to each possible decision.

Now, reset <- 3 and mynumber <- 4 either directly in the console or from the editor. When you run the mynumber example code, you'll get the following output:

First condition was TRUE
Second condition was TRUE

```R
R> a
[1] 9
R> b
[1] 1.000000 3.666667 6.333333 9.000000
```

> The result indicates which code was invoked—the first condition and second condition were both TRUE. Trying another run of the same code, after first setting

```R
R> a <- 6
R> mynumber <- 4
```

you see this output:

First condition was FALSE
Second condition was TRUE

```R
R> a
[1] 2.5
R> b
[1] 0.4
```

This time the first condition fails, but the second condition checked inside the else statement is TRUE. Alternatively, you could accomplish the same thing by sequentially stacking statements and using a combination of logical expressions in each condition. In the following example, you check for the four situations, but this time you stack statements by placing a new if following an else declaration:

```R
if(a<mynumber){
cat("First condition was TRUE\n")
a <- "a2"
if(mynumber>3){
cat("Second condition was TRUE\n")
b <- seq(1,a,length=mynumber)
} else {
cat("Second condition was FALSE\n")
b <- a-mynumber
}
} else {
cat("First condition was FALSE\n")
a <- a-3.5
if(mynumber>4){
cat("Second condition was TRUE\n")
b <- a*(3-mynumber)
} else {
cat("Second condition was FALSE\n")
b <- rep(a+mynumber,times=3)
}
```
