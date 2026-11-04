In this example, you increment the value of counter in an infinite do-while loop. To break out of the loop, you use a if statement to check the value of counter. If the value exceeds 100, you use the break keyword to exit the do-while loop.

You can also use the break keyword in while, for, and foreach loops.

# return

The return keyword allows you to terminate the execution of a method and return control to the calling method. When you use it within a loop, it will also exit from the loop. In the following example, the FindWord() function searches for a specified word ("car") inside a given array. As soon as a match is found, it exits from the loop and returns control to the calling method:

```
class Program
{
    static string FindWord(string[] arr, string word)
    {
        foreach (string w in arr)
        {
            //---if word is found, exit the loop and return back to the
            // calling function---
            if (w.StartsWith(word))
                return w;
        }
        return string.Empty;
    }

    static void Main(string[] args)
    {
        string[] words = {
            "-online", "4u", "adipex", "adviser", "baccarat", "blackjack",
            "blogspot", "booker", "bycb", "car-rental-e-site",
            "car-rentals-e-site", "carisoprodol", "casino", "casinos",
            "chatroom", "cialis", "coolcolhu", "coolhu", "credit-card-debt",
            "credit-report-4u"
        };

        Console.WriteLine(FindWord(words, "car")); //---car-rental-e-site---
    }
}
```

# throw

The throw keyword is usually used with the try-catch-finally statements to throw an exception. However, you can also use it to exit a loop prematurely. Consider the following block of code that contains the Sums() function to perform some addition and division on an array:

```
class Program
{
    static double Sums(int[] nums, int num)
    {
        double sum = 0;
        foreach (double n in nums)
```