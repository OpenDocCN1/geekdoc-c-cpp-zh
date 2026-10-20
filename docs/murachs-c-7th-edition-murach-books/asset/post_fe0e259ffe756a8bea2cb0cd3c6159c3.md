
## How to work with arrays

Now that you understand how to declare an array and assign values to its elements, you’re ready to learn how to work with the values in an array. Figure 8-3 presents some of the basic techniques for doing that.

This figure starts by presenting the Length property of an array, which gets the number of elements in the array. You’ll use this property frequently as you work with arrays.

The first example in this figure shows how to get the values from an array and calculate the average value of the elements. Here, the first statement declares a totals array that contains four decimal values. Then, the second statement sets the sum variable equal to the sum of the four elements in the array. Finally, the third statement computes the average value of these elements by dividing the sum by four.

The second example uses a for loop to put the numbers 0 through 9 into an array. Here, the first statement declares an array named numbers that contains 10 int values. Then, the for loop assigns the value of the loop’s counter to each of the elements in the array.

The third example uses a for loop to display the elements of the numbers array in a message box. Here, the first statement declares a string variable. Then, the for loop accesses each element of the numbers array and appends the number and a space to the string variable. When the for loop finishes, the next statement displays the string that contains the numbers in a message box.

The fourth example shows how to use a loop to calculate the average value of the elements in the totals array. Here, the first statement declares the sum variable. Then, the for loop gets the value of each element of the array and adds that value to the current value of the sum variable. After the loop, the next statement uses the sum variable and the Length property of the array to calculate the average. If you compare this code to the code in the first example, you’ll see that they both accomplish the same task. However, the code in this example will work equally well whether the totals array contains 4 or 400 values. As a result, it usually makes sense to use loops when working with arrays.

The last example shows how to display the elements of the totals array, along with the sum and average for the array, in a message box. Like the third example, this one uses a for loop to format the values in the array as a string. Then, it displays the string and the sum and average values in a message box.

### The syntax for using the Length property of an array

```
arrayName.Length
```

### Code that computes the average of an array of totals

```
decimal[] totals = {14.95m, 12.95m, 11.95m, 9.95m};
decimal sum = totals[0] + totals[1] + totals[2] + totals[3];
decimal average = sum/4;
```

### Code that puts the numbers 0 through 9 into an array

```
int[] numbers = new int[10];
for (int i = 0; i < numbers.Length; i++)
    numbers[i] = i;
```

### Code that displays the numbers array in a message box

```
string numbersString = "";
for (int i = 0; i < numbers.Length; i++)
    numbersString += numbers[i] + " ";
MessageBox.Show(numbersString, "Numbers Test");
```

![](img/844f608d10a44654833ea5efc8a2e7a7_252_0.png)

### Code that uses a for loop to compute the average of the totals array

```
decimal sum = 0.0m;
for (int i = 0; i < totals.Length; i++)
    sum += totals[i];
decimal average = sum/totals.Length;
```

### Code that displays the totals array in a message box

```
string totalsString = "";
for (int i = 0; i < totals.Length; i++)
    totalsString += totals[i] + "\n";
MessageBox.Show("The totals are:\n" +
    totalsString + "\n" +
    "Sum: " + sum + "\n" +
    "Average: " + average, "Totals Test");
```

![](img/844f608d10a44654833ea5efc8a2e7a7_252_1.png)

## How to use foreach loops to work with arrays

Although you can use for loops to work with the elements of an array, it’s often easier to use a foreach statement to code a foreach loop. Figure 8-4 shows how to do that.

To code a foreach loop, you begin by coding the foreach keyword followed by a set of parentheses. Within the parentheses, you code the data type of the elements in the array, the name you want to use to access the elements, the in keyword, and the name of the array. You can also code the var keyword in place of the data type, in which case the type is inferred from the type of the array.

Next, you can code one or more statements that use the element name to work with an element. If the foreach loop contains two or more statements, you must code braces around them. Otherwise, you can omit the braces.

When a foreach loop is executed, its statements are executed once for each element in the array. For instance, the first example in this figure shows how you can use a foreach loop to display the elements in the numbers array that you saw in the previous figure. Similarly, the second example computes the average of the totals array, and the third example displays the elements in the totals array.

If you compare these examples to the for loop examples in the previous figure, you’ll see that foreach loops are less complicated. In particular, when you use a foreach loop, you don’t need to use a counter variable, and you don’t need to use an index to get an element from the array. As a result, it’s often easier to use a foreach loop than a for loop.

You should realize, however, that there are still times when you’ll need to use a for loop to work with an array. For example, if you only want to access some of the elements in an array, you’ll need to use a for loop. You’ll also need to use a for loop if you want to use a counter variable to assign values to the elements of the array as shown in the second example in figure 8-3.

## How to work with rectangular arrays

So far, this chapter has shown how to work with an array that uses one index to store elements in a one-dimensional array. Now, you’ll learn how to work with rectangular arrays that use two indexes. You can think of a rectangular array as a table that has rows and columns. Since rectangular arrays store data in two dimensions, they’re also known as two-dimensional arrays.

Although it’s possible to create arrays that contain more than two dimensions, that’s rarely necessary. However, if you do need to use an array that has three or more dimensions, you can extend the two-dimensional techniques that you’ll learn next.

### How to create a rectangular array

Figure 8-5 shows how to create a rectangular array. To do that, you code a comma within the set of brackets that follows the data type declaration. This indicates that the array will have two dimensions. Then, when you use the new keyword to create the array, you specify the number of rows in the array, followed by a comma, followed by the number of columns in the array.

The first statement in this figure creates a rectangular array of integers. In this case, the array has three rows and two columns. After this statement executes, each element in the array will be assigned the default value of 0 as described in figure 8-1.

### How to assign values to a rectangular array

After you create an array, you can assign values to it. To do that, you refer to each element of the array using its row and column index. This is illustrated by the table of index values shown in figure 8-5. Because this array consists of four rows and four columns, the index values range from 0,0 to 3,3.

To assign values to the elements of a rectangular array, you can code one statement for each element as shown in the first example. These statements assign values to the elements of the numbers array that was created by the first statement in this figure.

You can also assign values to a rectangular array when you declare it, as illustrated by the second, third, and fourth examples. Here, the second example creates the numbers array and assigns values to it by coding three sets of braces within an outer set of braces. The three inner braces represent the three rows in the array, and the values in these braces are assigned to the two columns in each row. The third example works the same except that it uses string objects instead of int values. The fourth example also creates a string array, but it infers the data type from the specified values. Because of that, it uses the new keyword.
