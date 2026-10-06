
# Using a for Loop to Search an Array

One way to determine whether an itemOrdered value equals a value in the validValues array is to use a for statement to loop through the array and set a Boolean variable to true when a match is found:

```
for(int x = 0; x < validValues.Length; ++x)
  if(itemOrdered == validValues[x])
    isValidItem = true;
```

This type of search is a sequential search because each array element is examined in sequence. This simple for loop replaces the long series of if statements. What's more, if a company carries 1000 items instead of 10, then the list of valid items in the array must be altered, but the for statement does not change at all. As an added bonus, if you set up another array with the same number of elements and corresponding data, you can use the same subscript to access additional information. For example, if the 10 items your company carries 10 different prices, then you can set up an array to hold those prices as follows:

```
double[] prices = {0.89, 1.23, 3.50, 0.69...}; // and so on
```

The prices must appear in the same order as their corresponding item numbers in the validValues array. Now the for loop finds the valid item number also finds the price, as shown in the program in Figure 6-3. In other words, if the item is found in the second position in the validValues array, then you can find the correct price in the second position in the prices. In the program in Figure 6-3, the variable used as a subscript, x, is set to 0 and the Boolean isValidItem is false. In the shaded portion of the figure, while the subscript remains smaller than the length of the array of valid item numbers, the subscript is continuously increased so that subsequent array values can be tested. When a match is found between the user's item and an item in the array, isValidItem is set to true and the price of the item is stored in itemPrice. Figure 6-4 shows two typical program executions.

If you initialize parallel arrays, it is convenient to use spacing (as shown in Figure 6-3) so that the corresponding values visually align on the screen or printed page.

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_260_0.png)

Although parallel arrays can be very useful, they can also increase the likelihood of errors. Any time you make a change to one array, you must remember to make the corresponding change in its parallel array. As you continue to study C#, you will learn superior ways to correlate data items. For example, in the chapter "Using Classes and Objects," you will learn that you can encapsulate corresponding data items in objects and create arrays of objects.

# Searching an Array Using a Loop

```
using System;
using static System.Console;
class FindPriceWithForLoop
{
    static void Main()
    {
        int[] validValues = {101, 108, 201, 213, 266,
        304, 311, 409, 412};
        double[] prices = {0.89, 1.23, 3.50, 0.69, 5.79,
        3.19, 0.89, 1.26, 8.00};
        int itemOrdered;
        double itemPrice = 0;
        bool isValidItem = false;
        WriteLine("Please enter an item");
        itemOrdered = Convert.ToInt32(ReadLine());
        for(int x = 0; x < validValues.Length; ++x)
        {
            if(itemOrdered == validValues[x])
            {
                isValidItem = true;
                itemPrice = prices[x];
            }
        }
        if(isValidItem)
            WriteLine("Price is {0}", itemPrice);
        else
            WriteLine("Sorry - item not found");
    }
}
```

**Figure 6-3** The FindPriceWithForLoop program

| Please enter an item 266 | Please enter an item 267 |
|---|---|
| Price is 5.79 | Sorry - item not found |

**Figure 6-4** Two typical executions of the FindPriceWithForLoop program

# CHAPTER 6 Using Arrays

In the fourth statement of the Main() method in Figure 6-3, itemPrice is set to 0. Setting this variable is required because its value is later altered only if an item number match is found in the validValues array. When C determines that a variable's value is only set depending on an if statement, C will not allow you to display the variable because the compiler assumes that the if statement's Boolean expression could have been false and the variable might not have been set to a value.

# Improving a Loop's Efficiency

The code shown in Figure 6-3 can be made more efficient. Currently, the program compares every itemOrdered with each of the 10 validValues. Even when an itemOrdered is equivalent to the value in the validValues array (101), you always make nine additional cycles through comparing all the values. On each of these nine additional iterations, the comparison between itemOrdered and validValues[x] is always false. So when a match for an itemOrdered is found, the most efficient action is to break out of the for loop statements executed when the.

**Figure 6-5** Loop with early exit

# Searching an Array Using a Loop

In the code shown in 6-5, instead of a for loop, you can use a while loop to search the array. In a while loop, the condition is evaluated at the beginning of each iteration. If the condition is true, the loop body is executed. If the condition is false, the loop terminates. This is often useful when you do not know exactly how many iterations will be needed.

```csharp
while (x < validValues.Length && itemOrdered != validValues[x])
{
    x++;
}
```

# Using a while Loop to Search an Array

In the application of Figure 6-6, the variable used as a subscript, x, is set to 0 and the Boolean variable-isValidItem is false. In the shaded portion of the figure, while the subscript remains smaller than the length of the array of valid item numbers, and the user’s requested item does not match a valid item, the subscript is continuously increased so that subsequent array values can be tested. When a match is found between the user's item and an item in the array, isValidItem is set to true and the price of the item is stored in itemPrice. Figure 6-7 shows two executions of the program. In the first execution, a match is found; in the second, an invalid item is entered, so no match is found.

```csharp
using System;
using static System.Console;
class FindPriceWithWhileLoop {
    static void Main() {
        int x;
        string inputOrdered;
        int itemOrdered;
        double itemPrice = 0;
        bool isValidItem = false;
        int[] validValues = {101, 108, 201, 213, 266, 304, 311, 409, 412};
        double[] prices = {0.89, 1.26, 3.50, 0.69, 5.79, 3.19, 0.99, 0.89, 1.26, 8.00};
        Write("Enter item number ");
        inputOrdered = ReadLine();
        itemOrdered = Convert.ToInt32(inputOrdered);
        x = 0;
        while(x < validValues.Length && itemOrdered != validValues[x]) {
            x++;
        }
        if(x != validValues.Length) {
            isValidItem = true;
            itemPrice = prices[x];
        }
        if(isValidItem)
            WriteLine("{0} sells for {1}", itemOrdered, itemPrice.ToString("C"));
        else
            WriteLine("No such item as {0}", itemOrdered);
    }
}
```

**Figure 6-6** The FindPriceWithWhileLoop program that searches with a while loop
