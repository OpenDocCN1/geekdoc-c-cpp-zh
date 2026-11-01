```
{
    static void Main(string[] args)
    {
        Money cash1 = new Money();
        cash1.Amount = 40M;
        Console.WriteLine("cash1.ToString() returns: " + cash1.ToString());
        Console.ReadLine();
    }
    public class Money
    {
        private decimal amount;
        public decimal Amount
        {
            get
            {
                return amount;
            }
            set
            {
                amount = value;
            }
        }
        public override string ToString()
        {
            return "$" + Amount.ToString();
        }
    }
}
```

This example is here just to illustrate syntactical features of C#. C# already has a predefined type to represent currency amounts, decimal, so in real life, you wouldn't write a class to duplicate this functionality unless you wanted to add various other methods to it. And in many cases, due to formatting requirements, you'd probably use the String.Format() method (which is covered in Chapter 8) rather than ToString() to display a currency string.

In the Main() method, you first instantiate a Money object. The ToString() method is then called, which actually executes the override version of the method. Running this code gives the following results:

```
cash1.ToString() returns: $40
```

# EXTENSION METHODS

There are many ways to extend a class. If you have the source for the class, then inheritance, which is covered in Chapter 4, is a great way to add functionality to your objects. What if the source code isn't available? Extension methods can help by allowing you to change a class without requiring the source code for the class.

Extension methods are static methods that can appear to be part of a class without actually being in the source code for the class. Let's say that the Money class from the previous example needs to have a method AddToAmount(decimal amountToAdd). However, for whatever reason the original source for the assembly cannot be changed directly. All that you have to do is create a static class and add the AddToAmount method as a static method. Here is what the code would look like:

```
namespace Wrox
{
    public static class MoneyExtension
    {
        public static void AddToAmount(this Money money, decimal amountToAdd)
```