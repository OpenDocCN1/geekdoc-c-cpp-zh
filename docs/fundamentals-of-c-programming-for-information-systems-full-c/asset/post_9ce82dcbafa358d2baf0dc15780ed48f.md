
## Review Questions

- **6.11** You want to develop a form that allows the user to select one section of an introductory IS course from a list of all sections. The number of sections varies from semester to semester within the range 3 to 8. The prompt for the user on the form would be

  > Please select a section.

  Based on the standard practice, which one of the following controls would you use to let the user select a section: a ListBox, a set of CheckBoxes, a set of RadioButtons, or a ComboBox?

- **6.12** It is desired to develop a form that allows the user to select one or more days from a list of all seven days of a week. The prompt for the user on the form would be

  > Please select one or more days:

  Based on industry standards, which one of the following controls would you use to let the user select one or more days: a ListBox, a set of CheckBoxes, a set of RadioButtons, or a ComboBox?

- **6.13** A form displays a list of sports in a ListBox named lstSports. A user selects Basketball and Soccer from the list at runtime, as shown below:

  What would be the value of lstSports.SelectedItems(0)?

  ![](img/143bad48262566137acc9c41f668a88f_220_0.png)

- **6.14** A form displays a list of sports in a ListBox named lstSports. A user selects Basketball and Soccer from the list at runtime, as shown below:

  What would be the value of lstSports.Items(2)?

  ![](img/143bad48262566137acc9c41f668a88f_220_1.png)

## Exercises

### Exercise 6-1

Develop a form, Icecream.cs, as shown below:

![](img/143bad48262566137acc9c41f668a88f_221_0.png)

The form must let the user do the following:

- Specify the number of scoops (max three) using a ScrollBar, and display the specified number in a Label named lblScoops.
- Select the type of sundae from a list of sundaes (Ice Cream, Custard, Yogurt, etc.) displayed in a ComboBox sorted alphabetically. Because the items in this list may change over time, do not assume that, for example, the third item will remain as Yogurt.
- Use a CheckBox to specify whether the user wants nuts for topping.
- Compute the amount due.
- Clear all data so that the user can make another set of selections.
- Exit the form.

The amount due is given by

Cost of Sundae (Ice cream - $3.50; Custard - $3.75; Yogurt - $4.00) * Number of Scoops + Cost of Nuts (0.50)

Do not use defaults for the items to be specified by the user. Defaults make it difficult to check whether the user forgot to select an item.

### Exercise 6-2

A charitable organization uses volunteers to put on 10 to 15 different types of fund-raising events per year. Examples of the types of events are brat fry, walkathon, bake sale and golfing. A section of the volunteer signup form collects the following information:

- Name
- Types of events a person would like to volunteer for (a person may select one or more types)
- Number of hours available per week (The options are 5-10, 11-20, 21-30, 31-40.)
- Whether he/she is a new volunteer

Develop a form named Exercise 6.2 that collects the above information. Select appropriate controls based on the guidelines discussed in your textbook. Write the data entered by the user into a ListBox. If a volunteer is new, display the word “New”; if not, display the word “Experienced.” A sample of the display is shown below:

```
Name:      Sam Adamson

Events:

Walkathon
Golfing

Hours/week:   11-20

Status:      New
```

Do not specify default values for any control. Defaults make it difficult to check whether the user forgot to select an item.

## Arrays

The variables we used so far can store only one value at a time. So, if you want to store 30 test scores in memory and do computations with them simultaneously, you would have to declare 30 different variables.

A single array allows you to store multiple data items of the same type. For example, a single one-dimensional array can store all 30 scores at the same time. Because one-dimensional (1-D) arrays are the simplest type of arrays, we will discuss them first.

### Topics

| Section | Topic | Section | Topic |
|---|---|---|---|
| 7.1 | Introduction to One-Dimensional Arrays | 7.4 | Accessing Elements of an Array Using foreach Loop |
| 7.2 | Assigning a Value to an Element of an Array | 7.5 | Copying an Array |
| 7.3 | Accessing Elements of an Array Using the Index | 7.6 | Looking Up Values in an Array |

### 7.1 Introduction to One-Dimensional Arrays

An array can be thought of as a container of data with multiple storage locations or slots, one location for each data item. An array called testScore that stores 10 test scores may be represented as follows:

| testScore | 85 | 92 | 87 | 67 | 83 | 91 | 73 | 98 | 83 | 84 |
|---|---|---|---|---|---|---|---|---|---|---|
| Element number: (subscript or index) | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

Each storage location of the array is called an element. The elements are numbered consecutively, starting with zero. An individual element of an array is accessed using the array name, followed by the element number (subscript or index) in brackets. The subscript must be an integer. For example, testScore[0] refers to the first element of the array, that is, the number 85, testScore[1] refers to the second element of the array—that is, the number 92, and testScore[9] refers to the tenth element of the array, the number 84.

Different arrays can hold data items of different types, including numbers, strings, arrays and objects. However, within an array, all elements must be of the same type. Thus, an array is a collection of data items of the same type.

An array, like testScore, which can store one set of data, is called a one-dimensional (1-D) array. A two-dimensional (2-D) array, discussed later in Chapter 8, can store multiple sets of data, all of the same type.

### Value Types versus Reference Types

The integer, real and Boolean types we discussed in earlier chapters are called value types because each variable of these types holds the actual value assigned to that variable. Thus, the memory location allocated to a value type variable holds the actual value assigned to that variable.

By contrast, arrays (and other objects) are called reference types because each variable of these types holds only a reference to the data—that is, the memory location or address of the data, not the actual data. A variable that references an object, like an array, is called a reference variable. Let’s first look at the value types through some examples.

Consider two value type variables, previousSales and currentSales, declared below:

```
int previousSales, currentSales;
```

The effect of declaring the variables would be to store the default value zero in the memory locations for the two variables, as follows:

![](img/143bad48262566137acc9c41f668a88f_224_0.png)

Assigning a value for currentSales using the statement, currentSales = 245; stores the value in the memory location for currentSales, as represented below:

![](img/143bad48262566137acc9c41f668a88f_224_1.png)

When currentSales is assigned to previousSales using the statement

```
previousSales = currentSales;
```

the value from currentSales is copied to the memory location for previousSales, so that both locations store the same data, as shown:

![](img/143bad48262566137acc9c41f668a88f_224_2.png)

As discussed in Chapter 1, if you later change the value of currentSales using a statement like

```
currentSales = 300;
```

it will have no effect on the value of previousSales. The locations for the two variables will appear as follows:

![](img/143bad48262566137acc9c41f668a88f_224_3.png)

Now, let’s look at how arrays differ.

### Creating Arrays

Creating and using an array, which is a reference type, involves two steps:

1. Create the array object in memory to hold a set of data items, and
2. Create a variable, called reference variable, which references (holds the address of) the array, as shown in Figure 7.1

![](img/143bad48262566137acc9c41f668a88f_225_0.png)

Here is a statement that creates an array called testScore:

```
int[] testScore = new int[10];
```

The right hand side, `new int[10]`, creates an array in memory. Let’s look at each part:

The key word `new` creates a new object (in memory) of the type specified by `int[10]`, and returns the memory location of the new array.

The expression `int[10]` specifies that the object is an array of int type, and that the **array size is 10**—that is, the array has 10 elements whose indexes ranges from 0 to 9. When a new array is created, each element has the default value zero.

The left-hand side, `int[] testScore`, declares a reference variable that we can use to access the array. The pair of square brackets after the variable type is what distinguishes it from a value type variable and specifies that it is a variable to reference an array.

The = operator stores a reference to the array (memory location of the array) in the reference variable testScore.

Figure 7-2 represents the effect of executing the statement, `int[] testScore = new int[10]`, to create the array testScore and assign the reference to testScore.

![](img/143bad48262566137acc9c41f668a88f_225_1.png)

You may split the statement, `int[] testScore = new int[10]`, to two separate statements:

```
int[] testScore;
testScore = new int[10];
```

The first statement, `int[] testScore`, declares testScore as a variable to reference an int type array. The second statement, `testScore = new int[10]`, creates an int type array of size 10 using the key word new. The = operator assigns the memory location of the new array to testScore.
