are the most effective of the data types present in C because they have direct dealings with the memory that to say it points to a particular address in the memory.

Let us consider once again the internal structure of a variable declaration by considering the following example: int x=5. When this is done you know that a variable is associated with an integer with a value 5 and some space in the memory must be kept aside for storing it.

The internal representation can be depicted as below:

```
x 3456.
```

Above you will notice that the computer has allotted the memory location with the number 3456 to store the number 5. This number 3456 is the address of x where its value 5 is stored and whenever the program has to recall the value of x from the memory it uses the number 3456 to identify where its value is stored.

The point to be grasped here is that the & and * operator. All this while you have been using the above operators for different purposes. The & operator was used in the scanf() statements to accept the number entered by the user but here the & operator has a different function altogether.

By using this operator before any variable in the printf() statements the address of that particular variable is displayed.

```
printf(“Address of i=%d”, &i);
```

The above printf() statements prints the address value of i.

Address of i=8349. The other operator which you were introduced to was the * operator which was used by you as arithmetic operator of multiplication. But in pointer jargon it is called value at address operators. As the term suggests when this operator is used along with variable and its address symbol (&), the value which is present at the address of that particular variable is displayed.

```
printf(“value of i=%d”, *(&i));
```

The output would be as below:

```
Value of i= 5
```

In the above example you can see that the * is used outside the parentheses within which is enclosed the address of i? Note Printing the value of *(&i) is as equivalent as printing the value of i.