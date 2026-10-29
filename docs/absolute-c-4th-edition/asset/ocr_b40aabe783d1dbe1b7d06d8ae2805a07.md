```
void input();
void output();
int getMonthNumber() { return month; }
int getDay() { return day; }
private:
    int month;
    int day;
    void testDate();
};
```

+   8. No, it cannot be a static member function because it requires a calling object for the member variable `name`.

+   9. The program is legal. The output is
+   
+   ```text
+   0 1 2 3 4 5 6 7 8 9
+   ```
+   
+   Note that changing `v` does not change copy. A true independent copy is made with the assignment.
+   
+   ```cpp
+   copy = v;
+   ```

+   10. The size is the number of elements in a vector, while the capacity is number of elements for which there is memory allocated. Typically the capacity is larger than the size.

# PROGRAMMING PROJECTS

+   1. Define a class called Month that is an abstract data type for a month. Your class will have one member variable of type int to represent a month (1 for January, 2 for February, and so forth). Include all the following member functions: a constructor to set the month using the first three letters in the name of the month as three arguments, a constructor to set the month using an integer as an argument (1 for January, 2 for February, and so forth), a default constructor, an input function that reads the month as an integer, an input function that reads the month as the first three letters in the name of the month, an output function that outputs the month as an integer, an output function that outputs the month as the first three letters in the name of the month, and a member function that returns the next month as a value of type Month. Embed your class definition in a test program.

+   2. Redefine the implementation of the class Month described in Programming Project 1 (or do the definition for the first time, but do the implementation as described here). This time the month is implemented as three member variables of type char that store the first three letters in the name of the month. Embed your definition in a test program.

+   3. My mother always took a little red counter to the grocery store. The counter was used to keep tally of the amount of money she would have spent so far on that visit to the store if she bought everything in the basket. The counter had a four-digit display, increment buttons for each digit, and a reset button. An overflow indicator came up red if more money was entered than the $99.99 it would register. (This was a long time ago.)

![](bbox=[0.041, 0.559, 0.188, 0.634])