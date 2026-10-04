Using your loop, confirm the following:
i. That the result of using mynum <- 5 is 120
ii. That using mynum <- 12 yields 479001600
iii. That having mynum <- 0 correctly returns 1

c. Consider the following code, where the operations in the braced area of the while loop have been omitted:

```
mystring <- "R fever"
index <- 1
ecount <- 0
result <- mystring
while(ecount<2 && index<=nchar(mystring)){
  # several omitted operations #
}
result
```

Your task is to complete the code in the braced area so it inspects mystring character by character until it reaches the second instance of the letter e or the end of the string, whichever comes first. The result object should be the entire character string if there is no second e or the character string made up of all the characters up to, but not including, the second e if there is one. For example, mystring <- "R fever" should provide result as "R fev". This must be achieved by following these operations in the braces:

+   1. Use substr (Section 4.2.4) to extract the single character of mystring at position index.
2. Use a check for equality to determine whether this single-character string is either "e" OR "E". If so, increase ecount by 1.
3. Next, perform a separate check to see whether ecount is equal to 2. If so, use substr to set result equal to the characters between 1 and index-1 inclusive.
4. Increment index by 1.

Test your code—ensure the previous result for mystring <- "R fever". Furthermore, confirm the following:

+   - Using mystring <- "beautiful" provides result as "beautiful"
- Using mystring <- "ECCENTRIC" provides result as "ECC"
- Using mystring <- "E1Ab0rAt e" provides result as "E1Ab0rAt"
- Using mystring <- "eeeeek!" provides result as "e"

# 10.2.3 Implicit Looping with apply

In some situations, especially for relatively routine for loops (such as executing some function on each member of a list), you can avoid some of the details associated with explicit looping by using the apply function. The apply