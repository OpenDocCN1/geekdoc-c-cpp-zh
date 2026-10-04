# Chapter 7

# 377

The array name temp identifies the startingnlocation of the array

```
temp[0] temp[1] temp[2] temp[3] temp[4]
```

Skip over three elements tonget to the starting locationnoflement 3

Startnhere

**Figure 7.3** Accessing an array—element 3

must be within the valid subscript range defined when the array is declared. For example,
assuming i and j are int variables, the following subscribed variables are valid:

```
temp[i]
temp[2*i]
temp[j-i]
```

An advantage of using integer expressions as expressions is that it allows
sequencing through an array by using a loop. This makes statements such as the following
unnecessary:

```
sum = temp[0] + temp[1] + temp[2] + temp[3] + temp[4];
```

The subscript values can be replaced by a for loop counter to access each
element in the array. For example, the code

```
sum = 0; // initialize the sum to zero
for (i = 0; i < 5; i++) // add in a value
sum = sum + temp[i];
```

retrieves each element in the for loop and adds it to the sum. The variable i is
bused as both the counter and the index referenced. As i increases by one time
through the loop, the next element in the array is referenced. The procedure for adding array
elements in the for loop is similar to the accumulation procedure you have used before.

The advantage of using a for loop to sequence through an array becomes apparent when
working with larger arrays. For example, if the array contains 100 values rather than just
5, simply changing the number of iterations to 100 is enough to sequence through
the 100 elements and adds each temperature to the sum.

As another example of using a for loop to sequence through an array, say you want to
locate the maximum value in an array of 1000 elements named voltage. The procedure to
locate the maximum value is to assume initially that the first element in the array is the
largest number. Then, as you sequence through the array, the maximum is compared to each