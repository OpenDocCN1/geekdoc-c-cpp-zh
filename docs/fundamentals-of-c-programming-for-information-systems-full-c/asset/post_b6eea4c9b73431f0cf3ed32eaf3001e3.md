
## Review Question

8.3 The following data on customer orders (Customer#, Order#, Order Qty. Unit Price) is stored in a text file named Orders.txt.

0155, 76533, 3, 10.95
0140, 75446, 12, 8.50
0150, 75550, 1, 89.95
0145, 75648, 25, 2.50

Consider the following code that reads the data from the above file.

```csharp
StreamReader OrdersReader = new StreamReader("Orders.txt");
string[] fields;
while (OrdersReader.EndOfStream == false)
{
    currentLine = OrdersReader.ReadLine();
    fields = currentLine.Split(',');
}
lstDisplay.Items.Add(fields[1]);
```

What would be the output displayed in the ListBox lstDisplay?

## 8.3 Reading Data from Files into Arrays

Reading data from files on secondary storage devices like hard disks and flash drives is relatively slow compared to accessing data from arrays and variables, which are stored in the internal memory. So, if data that is stored in a file is to be accessed multiple times in a program, it generally would be more efficient to read the data from the file only once, store it in an array (or arrays), and access the array(s) for subsequent use of the data. For very large data sets, the consumption of internal memory by arrays should be weighed against the improvement in access speed.

A typical application that uses arrays is looking up information multiple times, like the phone number or address for different customers. Another application is computing the average for a field and then identifying all records that have above average values.

Let’s consider an expanded version of the ReadTextFiles form to display a list of all students whose percent score is above the class average as shown in Figure 8-8.

**Figure 8-8:** The ReadTextFiles form displaying above average students

![](img/143bad48262566137acc9c41f668a88f_254_0.png)

To find above average students, first you need to read all student records and compute the class average. Then, you need to access the same records again to identify who got scores above the class average.

Rather than reading the file twice, read the file once, compute the class average, and store student names in a one-dimensional array and the percent scores in another array. Then, use these arrays to identify those who got above average scores.

What array size should you use to create these arrays? The array size limits the number of data items that can be stored in an array. If a program needs to read data from a file with an increasing number of records over time, then the array size should be as large as the maximum number of records the file is likely to have. Similarly, if the program needs to read from files of different sizes, then the array size should be as large as the size of the largest file. For ease of viewing the arrays, this example limits the sizes of the two arrays to 10, as specified in the following statements that create the arrays.

```csharp
string[] names      = new string[10];
float[] percentScores = new float[10];
```

Storing data in the arrays involves the following process:

- Read the first record from Exams.txt and store the name in the first element of the names array, and store the percent score in the first element of the percentScores array, as shown in Figure 8-9.
- Read the second record from Exams.txt and store the name in the second element of the names array, and store the percent score in the second element of the percentScores array.

This process is repeated for each record in the file.

**Figure 8-9:** The names and percentScores arrays

| names {string[10]} | percentScores {float[10]} |
|----------------------|---------------------------|
| [0] "Mike Burns" | [0] 83.5 |
| [1] "Cathy Arnold" | [1] 90.5 |
| [2] "Wesley Mathews" | [2] 86 |
| [3] "Jerry Luke" | [3] 79.5 |
| [4] "Gina Rodriguez" | [4] 82.5 |
| [5] null | [5] 0 |
| [6] null | [6] 0 |
| [7] null | [7] 0 |
| [8] null | [8] 0 |
| [9] null | [9] 0 |

Figure 8-10 shows the first part of the code that reads and stores the data in the two arrays and computes the class average.

**Figure 8-10:** Code to compute class average using arrays

```csharp
65 private void btnAboveAvg_Click(object sender, EventArgs e)
66 {
67     //Declare two 1-D arrays
68     string[] names = new string[10];
69     float[] percentScores = new float[10];
70     // percentScores is the array of all percent scores
71     int recordCount, index = 0;
72
73     string currentLine;
74     string[] fields;
75     float percentScore, classTotal = 0, classAvg;
76     //percentScore is the percent score for a student;
77     StreamReader examsReader = new StreamReader("Exams.txt");
78
79     while (examsReader.EndOfStream == false)
80     {
81         currentLine = examsReader.ReadLine(); // read current line
82         fields = currentLine.Split(','); // split current line
83         percentScore = (float.Parse(fields[1]) + float.Parse(fields[2]))/2;
84
85         names[index] = fields[0]; //Store name into current element of names array
86         percentScores[index] = percentScore;  // Store percent into percentScores
87         index = index + 1;
88         classTotal = classTotal + percentScore; // Add current percent to classTotal
89     }
90     recordCount = index;
91     classAvg = classTotal / (float) recordCount;
```

Let’s examine the key statements of the code.

### Lines 81-83

```csharp
81 currentLine = examsReader.ReadLine(); // read current line
82 fields = currentLine.Split(','); // split current line
83 percentScore = (float.Parse(fields[1]) + float.Parse(fields[2]))/2;
```

This is identical to the code you used earlier in Figure 8-7 to compute and display the percent scores. This code reads each record, splits the record to three string type data items that are stored in fields array, and computes the percent score. The fields array, as discussed earlier, looks as follows after the first iteration through the loop:

![](img/143bad48262566137acc9c41f668a88f_255_0.png)

### Line 85

`names[index] = fields[0];` //Store name into current element of names array

To access each element of the names array, this statement uses the variable index, which is initialized to zero (line 71) and incremented by one within the loop (line 87).

The first time through the loop, names[index] refers to the first element, names[0], which is assigned the value of fields[0] that always represents the name from the current record. The statement in line 85 would be equivalent to

```csharp
names[0] = fields[0];
```

So, after the first iteration, the names array would look as follows:

![](img/143bad48262566137acc9c41f668a88f_256_0.png)

The second time through the loop, index is 1. So line 85 is equivalent to

```csharp
names[1] = fields[0];
```

So, the name from the second record is stored in the second element of names, as shown below:

![](img/143bad48262566137acc9c41f668a88f_256_1.png)

The third, fourth and fifth times, index becomes 2, 3 and 4, respectively; so line 85 would be equivalent to

```csharp
names[2] = fields[0];
names[3] = fields[0];
names[4] = fields[0];
```

After all records are read during the first five iterations of the loop, the array will have names stored in the first five elements as follows:

![](img/143bad48262566137acc9c41f668a88f_256_2.png)

### Line 86

`percentScores[index] = percentScore;` //Store percent into percentScores

This statement is similar to the previous one except that it stores the current student’s percent score in the current element of percentScores array. Because the value of index increments by one each time through the loop, line 86 would be equivalent to

```csharp
percentScores[0] = percentScore;
percentScores[1] = percentScore;
percentScores[2] = percentScore;
etc.
```

After the loop is completed, percentScores will have all five percents stored in the array as follows:

| percentScores {float[10]} |
|---------------------------|
| [0] 83.5 |
| [1] 90.5 |
| [2] 86 |
| [3] 79.5 |
| [4] 82.5 |
| [5] 0 |
| [6] 0 |
| [7] 0 |
| [8] 0 |
| [9] 0 |

### Line 88

`classTotal = classTotal + percentScore;`

This line calculates a running total of the percent scores for all student records that were read. The variable classTotal that accumulates the percent scores must be initialized (see line 75).

### Lines 90-91

```csharp
90 recordCount = index;
91 classAvg = classTotal / (float) recordCount;
```

Because index is reinitialized to zero in the next part (not shown in Figure 8-10), its current value (that gives the number of records read) is stored in another variable, recordCount.

- Step 1-9: Open the Click event handler of btnAboveAvg. Add the missing code from lines 85–91 in Figure 8-10.
- Step 1-10: Put a break at the end of the loop on line 89, and run the project.
  - Click ComputeAvg button, and observe the values of names, percentScores and fields arrays each time through the loop.

### Identifying Above Average Students

To identify students whose percent score is above the class average, the class average is compared to each element of percentScore array, using a loop. If an element is above class average, the corresponding element from the names array is displayed. For example if percentScore[2] is above average, names[2] is displayed.

This method works only if the two arrays are loaded consistently so that there is a one-to-one correspondence between the elements of names and those of percentScores (i.e., percentScores[0] is the percent for names[0], percent[1] represents the percent for names[1], etc).
