# Chapter 13: Delegates and Lambda Expressions

original code in Listing 13.8, which the anonymous function syntax was intended to streamline. However, the code transformation performed by the compiler can be considerably more complex than rewriting the anonymous function as a static method if outer variables are involved.

# Outer Variables

Local variables declared outside a lambda expression (including parameters of The containing method) are called the outer variables of that lambda. (This reference, though technically not a variable, is also considered to be an outer variable.) When a lambda body uses an outer variable, the variable is said to be captured (or, equivalently, closed over) by the lambda. In Listing 13.20, we use an outer variable to count how many times BubbleSort() performs a comparison. Output 13.2 shows the results of this listing.

# Listing 13.20: Using an Outer Variable in a Lambda Expression

```
public class Program
{
    public static void Main()
    {
        int[] items = new int[5];
        int comparisonCount = 0;

        for (int i = 0; i < items.Length; i++)
        {
            Console.Write("Enter an integer:");
            string text = Console.ReadLine();
            if (!int.TryParse(text, out items[i]))
            {
                Console.WriteLine($"{text}" is not a valid integer.");
                return;
            }
        }
    }

    DelegateSample.BubbleSort(items,
        (int first, int second) =>
        {
            comparisonCount++;
            return first < second;
        });
```