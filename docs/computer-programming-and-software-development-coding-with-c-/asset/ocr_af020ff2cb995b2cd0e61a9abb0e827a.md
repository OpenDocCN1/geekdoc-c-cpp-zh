add the bonus afterwards. If we run this again, we should see 1000 more. That seems to be correct. There are other assignment operators. One that I particularly like is the following. Say that I want to add to ratePerHour, let's say, 3. We want to increase the rate per hour. I can do that as follows by saying +=, and then I say 3. This is the same as saying that ratePerHour = the result of ratePerHour, the current value that is, plus 3. This assignment operator is a shortcut I use frequently. It's a simple way to increase the current value of this ratePerHour variable with 3.

We can also do equality operators in C#. I can, for example, use the currentMonthWage value and do a check with an if statement to see if the value is larger than 2000. And based on this, I'm going to again to write something to the console. Another operator that is frequently used is the double plus or double minus.

```
namespace BethanysPieShopHRM
{
    class Program
    {
        static void Main(string[] args)
        {
            int monthlyWage = 1234;
            int months = 12, bonus = 1000;

            bool isActive = true;
            double rating = 99.25;

            double ratePerHour = 12.34;
            int numberOfHoursWorked = 165;

            double currentMonthWage = ratePerHour * numberOfHoursWorked + bonus;

            Console.WriteLine(currentMonthWage);

            Console.ReadLine();
        }
}
```