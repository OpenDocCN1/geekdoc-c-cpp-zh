
```c
double[] total = { 0, 0, 0, 0 };
private void OkButton_Click(object sender, EventArgs e) {
    int dept;
    double contribution;
    dept = Convert.ToInt32(deptTextBox.Text);
    contribution = Convert.ToDouble(contributionTextBox.Text);
    --dept;
    total[dept] += contribution;
    deptTextBox.Text = "";
    contributionTextBox.Text = "";
}
private void DoneButton_Click(object sender, EventArgs e) {
    outputLabel.Text = "Dept Total";
    for (int x = 0; x < total.Length; x++) {
        outputLabel.Text += String.Format("\n{0}: {1}", x + 1, total[x].ToString("C"));
    }
}
```

**Figure 6-24** Code that declares array and two methods needed for the CountContributions application

## TWO TRUTHS & A LIE

## Array Issues in GUI Programs

- 1. A GUI program can contain declarations for any number of arrays of any data type.
- 2. If a method reacts to a user-initiated event, it cannot contain an array declaration.
- 3. If a method reacts to a user-initiated event and the method contains an array declaration, the array will be redeclared with each event occurrence.

> The false statement is #2. If a method reacts to a user-initiated event, it cannot store data that must persist over a number of events. The only problem is that the array will be redeclared with each new event.

## Chapter Summary

- An array is a list of data items, all of which have the same type and the same name but are distinguished from each other using a subscript or index. You declare an array variable by inserting a pair of square brackets after the type and reserve memory for an array by using the keyword **new**. Any array elements are numbered 0 through one less than the array's length. In **C#, arrays are objects derived from a class **System.Array**. An array's elements are initialized to default values. To initialize an nondefault values, you use a list of values that are separated by commas and enclosed within curly braces.

- Arrays are most powerful when variables are used to process array elements. Any array element subscript must remain in the range of 0 through **Length** - 1. The **Length** property automatically holds an array's length. You can use the **foreach** statement to cycle through every array element without using subscripts.

- When you want to determine whether a variable holds one of many possible values, you can compare the variable to a list of values in array. You can set up a parallel array to access additional information.

- The **BinarySearch()** method finds a requested value in a sorted array. The method returns -1 if the value is not found in the array; otherwise, it returns the position of the sought value. The **Sort()** method arranges arrays in ascending order. **Reverse()** reverses the order of items in an array.

- C# supports multidimensional arrays that require multiple subscripts to access array elements. The most commonly used multidimensional arrays are two-dimensional arrays that are rectangular. Two-dimensional arrays have two or more columns of values for each row. In a rectangular array, each row has the same number of columns. C# also supports jagged arrays, which are arrays of arrays.

- The most unusual consideration when using an array in a GUI program is that if the array values change based on user input, the array must be stored outside any method that reacts to the user's event.

## Key Terms

An **array** is a list of data items that have the same data type and the same name but are distinguished from each other by a subscript or index.

An **array element** is an individual object within array.

A **subscript** (also called **index**) is an integer contained within square brackets that indicates the position of an array's elements.

An **initializer list** is the list of values provided for an array.

Read-only describes a value that can be accessed but not altered.

An iteration variable is a temporary location that holds each array value in turn in a foreach statement.

A sequential search is conducted by examining a list in sequence.

A parallel array has the same number of elements as another array and corresponding data.

A range match determines the pair of limiting values between which a value falls.

A binary search is an algorithm that finds an item in a list by splitting the sorted list of objects in half repeatedly until the search gets closer to a match.

A one-dimensional or single-dimensional array is an whose elements you can access using a single subscript.

Multidimensional arrays require multiple subscripts to access the array elements.

Two-dimensional arrays have two or more columns of values for each row.

A rectangular array is an array in which each row has the same number of columns.

A jagged array is a one-dimensional array in which each element is another array.

## Review Questions

- 1. In an array, every element has the same
  a. subscript
  c. data type
  b. memory location
  d. all of the above

- 2. The operator used to create objects
  a. =
  c. new
  b. +=
  d. create

- 3. Which of the following correctly declares an array of six integers?
  a. int array[6];
  c. int[6] array;
  b. int[] array = 6;
  d. int[] array = new int[6];

- 4. The value placed within square brackets after an array name is
  a. always a constant
  c. called a subscript
  b. always a double
  d. all of these

- 5. If you define an array to contain 10 elements, then the highest array subscript you can use is ________________
  a. 8	c. 10
  b. 9	d. 11

- 6. Initializing an array is in C# ________________
  a. optional	c. difficult
  b. required	d. prohibited

- 7. When you declare an array of six double elements but provide no initialization values, the value of the first element is ________________
  a. 0.0	c. 5.0
  b. 1.0	d. unknown

- 8. Which of the[] ages correctly declares an array of four integers?
  a. int[] ages = new int[4]{20, 30, 40, 50};
  b. int[] ages = new int[] {20, 30, 40, 50};
  c. int[] ages = {20, 30, 40, 50};
  d. all of these

- 9. When an ages array is correctly initialized using the values {20, 30, 40, 50}, then the value of ages[1] is ________________
  a. 0	c. 30
  b. 20	d. undefined

- 10. When an ages array is correctly initialized using the values {20, 30, 40, 50}, then the value of ages[4] is ________________
  a. 0	c. 50
  b. 4	d. undefined

- 11. When you declare an array as int[] temperature = {0, 32, 50, 90, 212, 451};, the value of temperature.length is ________________
  a. 5	c. 7
  b. 6	d. unknown

- 12. Which of the following doubles every value in a 10-element integer array named amount?
  a. for(int x = 9; x >= 0; x--) amount[x] *= 2;
  b. foreach(int number in amount) number *= 2;
  c. both of these
  d. neither

- 13. Which of the following adds 10 to a 16-element array?
  a. for(int sub = 0; sub < 16; sub++) points[sub] += 10;
  b. foreach(int sub in points) sub += 10;
  c. both of these
  d. neither

- 14. Two arrays that store related information in corresponding positions.
  a. jagged
  c. parallel
  b. rectangular

- 15. Assume an array is defined as int[] nums = {2, 3, 4, 5}; Which of the following would display the array in reverse?
  a. for(int x = 4; x > 0; x--) Write(nums[x]);
  b. for(int x = 3; x >= 0; x--) Write(nums[x]);
  c. for(int x = 3; x > 0; x--) Write(nums[x]);
  d. for(int x = 4; x >= 0; x--) Write(nums[x]);

- 16. Assume an array is defined as int[] nums = {7, 15, 23, 5, 5}; Which of the following would place the values in the array in descending order?
  a. Array.Sort(nums);
  b. Array.Reverse(nums);
  c. Array.Sort(nums); Array.Reverse(nums);
  d. both of the above

- 17. Which of the following traits do the BinarySearch() and Sort() methods have common?
  a. Both methods take a single argument that must be an array.
  b. They both operate on arrays made up of numeric data.
  c. The array that each method uses must start in ascending order.
  d. Both methods belong to System.Array class.

- 18. If you use the BinarySearch() method, and the object you seek is not found in the array,
  a. an error message is displayed
  b. a zero is returned
  c. the value false is returned
  d. a negative value is returned

- 19. The BinarySearch() method is inadequate when
  a. array items are in ascending order
  b. the array holds duplicate values and you want to find them all
  c. you want to find an exact match for a value
  d. array items are not numeric

- 20. Which of the following declares an integer array that contains eight rows and five columns?
  a. int[8, 5] num = new int[,];
  b. int[8][5] num = new int[];
  c. int[ , ] num = new int[5, 8];
  d. int[ , ] num = new int[8, 5];

## Exercises

## Programming Exercises

For each of the following exercises, you may choose to write a console-based or GUI application, or both.

- 1. Write a program named ArrayDemo that stores an array of 10 integers. Until the user enters a sentinel value, allow the user four options: (1) to view the list in order from the first to last position in the stored array, (2) to view the list in order from the last to first position, (3) to choose a specific position to view, or (4) to quit the application.
