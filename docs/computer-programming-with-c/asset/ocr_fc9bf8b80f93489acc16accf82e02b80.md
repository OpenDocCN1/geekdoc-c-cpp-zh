```
```c
{"Zero","One","Two","Three","Four","Five","Six","Seven","Eight","Nine"};
int s=0,x,d, a[100];
int w;
printf("Enter a number: ");
scanf("%d",&x);
int i=0;
while(x!=0)
{
    d=x%10; //get the individual digit
    a[i]=d;
    i++;
    x=x/10;  //Use quotient for the next addition
}
/*Traverse the array in reverse direction*/
printf("The word format is: ");
for(w=i-1;w>=0;w--)
{
    printf("%s ",words[a[w]]);
}
}
```
```

# Output

Enter a number: 1265

The word format is: One Two Six Five

# The statement

```
```c
char words[ ][15]=
{"Zero","One","Two","Three","Four","Five","Six","Seven",
"Eight","Nine" };
```
```

creates an array of strings which stores each digit in the word format as shown in Figure 6.39.

# The statements

```
```c
printf("Enter a number: ");
scanf("%d",&x);
```
```

accept a number x as input from the user which is to be translated into words.

We have used division by 10 to extract individual digits of x. Each digit extracted by the while loop is stored in an array a. The digit extraction logic is very similar to what we have designed in Chapter 5, Section 5.2.4. Hence, the digits will be extracted in the reverse order. So, if the input value x is 1265 the array a will contain the digits in reverse order as shown in Figure 6.40.

Therefore, to translate each of the digits into words, we will have to iterate over the array in a reverse direction (last element of the array must be visited first, so that we get the correct order back).

**Array words**

| Index | Value |
|---:|---|
| 0 | "Zero" |
| 1 | "One" |
| 2 | "Two" |
| 3 | "Three" |
| 4 | "Four" |
| 5 | "Five" |
| 6 | "Six" |
| 7 | "Seven" |
| 8 | "Eight" |
| 9 | "Nine" |

*Figure 6.39: Array words*

**Array a**

| 5 | 6 | 2 | 1 |
|---:|---:|---:|---:|
| 0 | 1 | 2 | 3 |

*Figure 6.40: Array a*