# Sorting Arrays

*Sorting*, as related to an array, is the action of rearranging or reorganizing the order of elements to make a particular task easier to follow. This usually involves some logical reference point such as letters placed in alphabetical order and numbers listed in a numeric order. The principle method used to displace these values involves both comparison and reassignment of that data. The techniques used to sort these values range from the very simple to the complex, but they all do pretty much the same thing; thus, the need for alternate techniques then has more to do with the speed of the process than the result. The simplest of these is known as the *bubble sort* (also referred to as the *sinking sort*); values are listed in a single array, compared with one another and swapped as needed, until all the values are in the proper order. The word bubble is used to aid in visualizing the smaller (lighter) values rising to the top and the word sinking is used to visualize the larger (heavier) values sinking to the bottom. The sort is also very straightforward—see Example 4.19.

# Example 4.19. Bubble sort.

```
using System;

namespace Chapter4 {
    class Class1 {
        static void Main() {
            const short array_size = 12;
            int[] simple_array = new int[array_size] {
                31, 31, 54, 0, 60, 35, 34, 29, 18, 17, 13, 10};

            BubbleSort (simple_array, array_size);
        }

        static void BubbleSort (int[] my_array, short size) {
            int temp = 0;
            Console.WriteLine("\nRandom numbers inputted in this order");

            for (int i = 0; i < size; i++)
                Console.WriteLine("{0}  ", my_array[i]);
            for (int i = 0; i < size; i++)
                for (int j = 0; j < size-1; j++)
                    if (my_array[j] > my_array[j+1]) {
                        temp = my_array[j];
```