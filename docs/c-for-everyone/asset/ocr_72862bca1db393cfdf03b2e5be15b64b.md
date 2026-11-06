```
```cpp
/**
 * @param factor the value with which each element is multiplied
 */
void multiply(double values[], int size, double factor)
{
   for (int i = 0; i < size; i++)
   {
      values[i] = values[i] * factor;
   }
}

/**
 * Prints the elements of a vector, separated by commas.
 * @param values a partially filled array
 * @param size the number of elements in values
 */
void print(double values[], int size)
{
   for (int i = 0; i < size; i++)
   {
      if (i > 0) { cout << ", "; }
      cout << values[i];
   }
   cout << endl;
}

int main()
{
   const int CAPACITY = 1000;
   double values[CAPACITY];
   int size = read_inputs(values, CAPACITY);
   multiply(values, size, 2);
   print(values, size);

   return 0;
}
```
```

# Program Run

```
```text
Please enter values, Q to quit:
12 25 20 Q
24, 50, 40
```
```

![](bbox=[0.077, 0.674, 0.226, 0.765])

+   15. What happens if you call the sum function and you lie about the size? For example, calling
+       `double result = sum(values, 1000);`
+       even though values has size 100.
+   
+   16. How do you call the squares function to compute the first five squares and store the result in an array numbers?
+   
+   17. Write a function that returns the first position of an element in an array, or −1 if the element is not present. Use the linear search algorithm of Section 6.2.6.
+   
+   18. Rewrite the `read_inputs` function so that the array size is a reference parameter, not a return value.
+   
+   19. Write the header for a function that appends two arrays into another array. Do not implement the function.