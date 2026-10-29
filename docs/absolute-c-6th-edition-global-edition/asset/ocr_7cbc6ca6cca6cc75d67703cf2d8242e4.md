# Display 5.9 Bubble Sort Program (part 2 of 2)

```
25 {
26     // Bubble largest number toward the right
27     for (int i = length-1; i > 0; i--)
28         for (int j = 0; j < i; j++)
29             if (arr[j] > arr[j+1])
30             {
31                 // Swap the numbers
32                 int temp = arr[j+1];
33                 arr[j+1] = arr[j];
34                 arr[j] = temp;
35             }
36 }
```

# Sample Dialogue

1 2 3 5 9 10

# Self-Test Exercises

17. Write a program that will read up to ten nonnegative integers into an array called numberArray, and then write the integers back to the screen. For this exercise you need not use any functions. This is just a toy program and can be very minimal.

18. Write a program that will read up to ten letters into an array and write the letters back to the screen in the reverse order. For example, if the input is abcd. then the output should be dcba Use a period as a sentinel value to mark the end of the input. Call the array letterBox. For this exercise you need not use any functions. This is just a toy program and can be very minimal.

19. Following is the declaration for an alternative version of the function search defined in Display 5.6. In order to use this alternative version of the search function we would need to rewrite the program slightly, but for this exercise all you need do is write the function definition for this alternative version of search.