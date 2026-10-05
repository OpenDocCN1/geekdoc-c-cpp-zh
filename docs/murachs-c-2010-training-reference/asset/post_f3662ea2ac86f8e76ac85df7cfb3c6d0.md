
# Chapter 8 How to work with arrays and collections

## The syntax for retrieving a value from an array list

(type) arrayName[index]

### Code that creates an array list that holds decimal values

```csharp
decimal[] salesTotals = {3275.68m, 4398.55m, 5289.75m, 1933.98m};
ArrayList salesTotals = new ArrayList();
foreach (decimal d in salesTotals)
    salesTotals.Add(d);
```

### Another way to create the array list

```csharp
ArrayList salesTotals = new ArrayList
{ 3275.68m, 4398.55m, 5289.75m, 1933.98m };
```

### Code that retrieves the first value from the array list

```csharp
decimal sales1 = (decimal) salesTotals[0]; // sales1 = 3275.68
```

### Code that inserts and removes an element from the array list

```csharp
salesTotals.Insert(0, 2745.73); // insert a new element
sales1 = (decimal) salesTotals[0]; // sales1 = 2745.73
decimal sales2 = (decimal) salesTotals[1]; // sales2 = 3275.68
sales2.RemoveAt(1); // remove the second element
sales2 = (decimal) salesTotals[1]; // sales2 = 4398.55
```

### Code that displays the array list in a message box

```csharp
string salesTotalsString = "";
foreach (decimal d in salesTotals)
    salesTotalsString += d + "\n";
MessageBox.Show(salesTotalsString, "Sales Totals");
```

![](img/3148667e42d4db35b3d08576aaa1fa01_268_0.png)

### Code that checks for an element in the array list and removes it if it exists

```csharp
decimal x = 2745.73;
if (salesTotals.Contains(x))
    salesTotals.Remove(x);
```

### Code that sorts and searches the array list

```csharp
salesTotals.Sort();
int sales2Index = salesTotals.BinarySearch(sales2);
```

### Description

- The ArrayList class is part of the System.Collections namespace.
- The ArrayList class has the same properties and methods as the List<T> class in the System.Collections.Generic namespace. As a result, it's easy to convert code that uses the ArrayList class to use the List<T> class and vice versa.

Figure 8-17 How to work with an array list

## Perspective

In this chapter, you've learned how to use both arrays and collections for working with groups of related data. You've also learned that the .NET Framework provides several different classes that offer useful properties and methods for working with arrays and collections. These include the Array, List<>, SortedList<>, Queue<>, Stack<>, and ArrayList.

As you develop your own applications, you need to decide between the use of an array or collection. Then, if you decide to use a collection, you need to choose the most appropriate type of collection. If you make the right decisions, your code will be easier to write, debug, and maintain.

## Terms

- array
- element
- length
- size
- one-dimensional array
- index
- upper bound
- foreach statement
- foreach loop
- rectangular array
- two-dimensional array
- jagged array
- array of arrays
- immutable
- collection
- mutable
- typed collection
- generics
- untyped collection
- using statement
- list
- collection initializer
- sorted list
- queue
- stack
- first-in first-out
- FIFO
- last-in first-out
- LIFO
- array list
- boxing
- unboxing

## Exercise 8-1 Use an array and a list

This exercise will guide you through the process of adding an array and a list to the Invoice Total application that you enhanced in the last chapter.

Open the Invoice Total application

1. Open the Invoice Total application that's in the C:\C# 2010\08\InvoiceTotal directory.
2. Declare two class variables: (1) an array that can hold up to five invoice totals and (2) an index that you can use to work with that array.
3. Add code that adds the total to the next element in the array each time the user clicks the Calculate button.
4. Add code that displays all the invoice totals in the array in a message box when the user clicks the Exit button. To do that, use a foreach loop to loop through the totals and format the message for the message box. Within this loop, you should include an if statement so that you only display totals that are not equal to zero.
5. Test the program by entering subtotals up to five invoices and clicking the Exit button. This should display a dialog box like this one:

![](img/3148667e42d4db35b3d08576aaa1fa01_270_0.png)

6. Test the program by entering more than five invoices. When you do, an IndexOutOfRangeException should be thrown. Then, modify the try-catch statement so it handles this exception.

Sort the invoice totals

7. Add code to sort the invoice totals.
8. Test the program to ensure the output is correct.

Modify the program so it uses a list

9. Without changing any code, repeat steps 2-8 but use a list.
10. Test the program to ensure the output is correct.

## Exercise 8-2 Use an array and a list

This exercise will guide you through the process of adding an array and a list to the Invoice Total application that you enhanced in the last chapter.

Open the Invoice Total application

1. Open the Invoice Total application that's in the C:\C# 2010\08\InvoiceTotal directory.
2. Declare two class variables: (1) an array that can hold up to five invoice totals and (2) an index that you can use to work with that array.
3. Add code that adds the total to the next element in the array each time the user clicks the Calculate button.
4. Add code that displays all the invoice totals in the array in a message box when the user clicks the Exit button. To do that, use a foreach loop to loop through the totals and format the message for the message box. Within this loop, you should include an if statement so that you only display totals that are not equal to zero.
5. Test the program by entering subtotals up to five invoices and clicking the Exit button. This should display a dialog box like this one:

![](img/3148667e42d4db35b3d08576aaa1fa01_270_0.png)

6. Test the program by entering more than five invoices. When you do, an IndexOutOfRangeException should be thrown. Then, modify the try-catch statement so it handles this exception.

Sort the invoice totals

7. Add code to sort the invoice totals.
8. Test the program to ensure the output is correct.

Modify the program so it uses a list

9. Without changing any code, repeat steps 2-8 but use a list.
10. Test the program to ensure the output is correct.
