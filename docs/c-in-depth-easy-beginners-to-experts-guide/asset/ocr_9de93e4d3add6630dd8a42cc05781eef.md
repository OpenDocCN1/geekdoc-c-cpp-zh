# Output: hello

First i is assigned with 5 that is non zero and assume true now second condition (z>=5) is checked and it is true so both condition are true and finally generate the true so the statement under if is executed and message “hello” is printed.

```
3. int i =4,j = -1,k =0,w,x,y,z;
    w = i||j||k;
    x = i&&j&&k;
    y = i||j&&k;
    z = i&&j||k
    printf("\nw=%d x=%d y=%d z=%d",w,x,y,z);
```

# Output: w =1 x =0 y =1 z =1

i =4 that is a non zero value means true condition.
j = -1 that is also a non zero value means true condition.
k =0 that means false condition.

```
4. int i =4,j = -1,k =0,y,z;
    y =j+5&&j+1||k+2;
    z = i+5 || j+1 && k+2;
    printf("\n y =%d z =%d",y,z);
```

# Output: 1 1

In the first statement j+5 =4(T) and j+1 =0(F) and k+2 =2(T) Now first (j+5 && j+1) □ (4 && 0) gives 0 (F) and second comparison will be (0 || k+2) □ (0||2) □ 1(T) so y =1.
In the second statement i+5 =9 and in the exp. (i+5 || j+1 && k+2) □ (9|| j+1&& k+2) and we know in the

are represented in IEEE format. The Ieee format for floating point storage uses a sign bit, a mantissa and an exponent for representing the power of 2. the sign bit denotes the sign of the number: a 0 represents a positive value and a 1 denotes a negative value. The mantissa is represented in binary after converting it to its normalized form. The normalized form results in a mantissa whose most significant digit is always 1. the IEEE format takes advantage by not storing this bit at all. The exponent is the integer stored in unsigned binary format after adding a positive integer bias. This ensures that the stored exponent is always positive. The value of the bias is 127 for floats and 1023 for doubles

```
16. int p = 8, q = 20;
    if(p == 5 && q<5)
        printf("Hello Matrix");
    else
        printf("Bye Matrix");
```

# Output: Bye Matrix

At first compiler execute the exp in if and there the first compare p == 5 that gives false(0) and here && is involve in exp, so control jumps out without checking for the next condition and gives false in if. Now because there is false condition in if control jumps to the else block and printed “Bye Matrix”.

```
17. int i = -1, j = 1,k,l;
```