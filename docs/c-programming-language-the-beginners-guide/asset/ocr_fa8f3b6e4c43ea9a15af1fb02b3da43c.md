This is basically a modification of existing code, switching values from *int* to as well as the associated placeholders. The value 5.0 is assigned to variable *b* at line 6. Remember, floating points have a decimal part. When you’re writing a whole number, you need to specify a “.0” after the value. Now build and run the code. Try the value 9 again. The result is more palatable, but ugly. In a later chapter, we’ll discuss how to clean up the output of floating point values. Now take a look at the code below:

```
```c
1  #include 2

3  int main()
4  {
5  int x = 10;
6
7  printf("%d\\n",x);
8  x = x + 1;
9  printf("%d\\n",x); 10
11 return(0);
12 }
13
```
```

Math is present at line 8. It adds one to the value of variable This equation may look funky to you, but it’s how it works. The compiler calculates the right side of the equation first. 1 is added to the value of variable That result is then stored back to the value of variable To prove how it works, build and run the code.