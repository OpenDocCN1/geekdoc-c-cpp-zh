
# Analysis

In Lesson 6, you saw a program that used a nested for statement; this program has two nested for loops. Before you look at the for statements in detail, note that lines 7 and 8 declare variables. The first is an array named random_array, used to hold random numbers. random_array is a three-dimensional type int that is 10-by-10-by-10, giving a total of 1000 int elements (10x10x10). Imagine coming with 1000 unique variable names if you couldn't use arrays! Line 8 declares three variables, a, b, and c, to control the for loops.

This program also includes the header file stdlib.h (for standard library). It is included to provide the prototype for the rand() function used on line 22.

The bulk of the program is contained in two nests of for statements. The first is in lines 16 through 25, and the second is in lines 29 through 42. Both for nests have the same structure. They work just like the loops in Listing 6.2, but they go one deeper. In the first set of for statements, line 22 is executed repeatedly. Line 22 assigns the value of c, rand(), to an element of the random_array array, where rand() is a library function that returns a random number.

Going backward through the list, you can see that line 20 changes c from 0 to 9. This loops through the farthest right subscript of the random_array array. Line 18 loops through b, the middle subscript of the random array. Each time b changes, it loops through all the c elements. Line 16 changes variable a, which loops through the farthest left subscript. Each time this subscript changes, it loops through all 10 values of b, which in turn loops through all 10 values of c. This initializes every value in the random array to a random number.

Lines 29 through 42 contain the second set of for statements. These work like the previous for statements, but these loops print each of the values assigned previously. After 10 are displayed, 38 prints a message and waits for Enter to be pressed. Line 40 takes care of the keypress using getchar(). If Enter hasn't been pressed, getchar() waits until it is. Run this program and watch the displayed values.

# Summary

This lesson introduced numeric arrays, a powerful data storage method under the same group name. Individual items, or elements, in an array are identified using a subscript after the array name. Computer programming tasks that involve repetitive data processing lend themselves to storage like nonarray variables, arrays must be declared before they can be used. Optionally, array elements can be initialized when the array is declared.

# Q&A

- What happens if I use a subscript on an array that is larger than the elements in the array?
- If you use a subscript that is out of bounds with the array declaration, the program will probably compile and even run. However, the results of such a mistake can be unpredictable. This could be a difficult error to find after it starts causing problems, make sure you're careful when initializing and accessing array elements.
- What happens if I use an array without initializing it?
- This mistake doesn't produce a compiler error. If you don't initialize an array, there can be any value in the array elements. You might get unpredictable results. You should always initialize variables and arrays so that you know exactly what's in them. Lesson 12 introduces you one exception to the need to initialize. For now, play it.
- How many dimensions can an array have?
- As stated in this lesson, you can have as many dimensions as you want. As you add more dimensions, use more data storage space. You should declare an array only as large as you need to avoid wasting storage space.
- Is there any easy way to initialize an entire array at once?
- Each element of an array must be initialized. The safest way for a beginner programmer to initialize an array is either with a declaration, as shown in this lesson, or with a for statement. There are other ways to initialize an array, but they are beyond the scope of this book.
- Can I add two arrays together (or multiply, divide, or subtract them)?
- If you declare two arrays, you can't add the two together. Each element must be added individually. Exercise 10 illustrates this point. You could, however, create a function that could add the two arrays together. Such a function will still be required.

# Workshop

The Workshop provides questions to help you solidify the material, and exercises to provide you with experience what you've learned.

# Quiz

- Which of C's data types can be used?
- In a 10-element array, what is the first subscript?
- If an array is declared with elements, what is the last element?
- What happens if your program tries to access an out-of-range?
- How do you declare a multidimensional array?
- How many elements does the array have?
- What would be the tenth element in array?

# Exercises

- Write a program that declares three-dimensional arrays, named one, two, and three, with 1,000 elements each.
- Given the following array, write code to initialize all elements to 1.
- Given the following array, write code to initialize all elements.
- Write a program that initializes an array of 10 elements. Each element should be equal to its subscript. The program should then print each of the 10 elements.
- Modify the program from exercise 9. After printing the initialized values, the program should copy the values to a new array and add 10 to each value. The new array values should be printed.

# 5. BUG BUSTER: What is wrong with the following code?

```
int x, y;
int array[10];
int main ( ) {
    for ( x = 0; x < 3; x++ )
        for ( y = 0; y < 10; y++)
            array[x][y] = 0;
}
```

# 6. BUG BUSTER: What is wrong with the following?

```
int array[10];
int x = 1;
int main( ) {
    for ( x = 1; x <= 10; x++)
        array[x] = 99;
}
```

# 7. Write a program that puts random numbers into a two-dimensional array that is 4. Print the values in columns. (Hint: Use the rand() function from 8.3.)

> Whenever you use the rand() function, it is a good idea to add the following line to the beginning of your program:
srand(time(NULL)); 
This call is needed to ensure every time you run the program you get random numbers. Believe it or not, there are times when a user would want to generate the same set of numbers (scientific experiments, for example), so the srand, short for seed, function is needed to ensure each time the program runs, it generates a new set of numbers.

# 8. Rewrite Listing 8.3 to use a single-dimensional array. Print the average of the 1,000 variables before printing the individual values. Note: Don't forget to pause after every 10 values are printed.
