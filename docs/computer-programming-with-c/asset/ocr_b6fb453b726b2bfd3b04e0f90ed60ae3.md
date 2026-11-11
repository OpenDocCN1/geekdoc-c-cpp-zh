# ### 6.3.2  Program to compute reverse of a string: An example

Let us create a program to accept a string as input from the user and to compute its reverse. For example, if user inputs a string as `hello`, then the program should compute the reverse as `olleh`. We create two arrays a and b such that array a will store the original string entered by the user and array b to store the reverse. As with all the other examples, we create character arrays a and b of size 100 assuming that user will not input any string with length greater than 100. We accept the string a as input from the user using the statements shown below:

```
```c
char a[100],b[100];
printf("Enter String\n");
scanf("%s",a);
```
```

Let us assume that the user enters a string value as `hello`; then the array a will be initialized as shown in Figure 6.25.

![](bbox=[0.56, 0.257, 0.789, 0.359])

**Figure 6.25:** Initialization of array a

Now, we need to calculate the reverse of array a and store it in array b. This means that a[4] must be copied to b[0], a[3] must be copied to b[1] and so on. Figure 6.26 gives the complete set of copy operations required to store the reverse of array a in array b. Note that the NULL character should always be present as the last character of both the strings a and b as shown in Figure 6.26.

We perform these copy operations using a `for` loop that copies each character in array a at an appropriate position in array b. Obviously, this means that the array a must be read in reverse direction and the array b must be written in forward direction by the program. Hence, the index of array a must start from the position of last character and should traverse it in the reverse order, whereas the index of array b must start from first position and traverse it in the forward direction.

Let variable k represent the position of last character in array a. Note that if length of the string stored in an array is 5, then the position of last character is 4 as seen from Figure 6.26; in general, if length of array a is `len` then the position of last character in array a is `len-1`. Hence, we initialize the initial value of variable k as shown below:

```
```c
int k= len-1; /*k is the position of last character in array a*/
```
```

![](bbox=[0.619, 0.498, 0.853, 0.722])

**Figure 6.26:** Calculating reverse of the string

It is clear that to determine the position of last character in string a we need to calculate length of a. Length of a string a can be easily calculated as discussed in Section 6.3.1. Also, let variable i represent the index of array b and hence the initial value of variable i must be set to zero as we need to initially write to the first location in array b. As the index position k must move in reverse direction the for loop must perform `k--` after each iteration.