book, but if you are interested, details are in the MSDN documentation.) The best answer is that you should design your casts so that all routes give the same answer (other than possible loss of precision), in which case it doesn't really matter which one the compiler picks. (As it happens in this case, the compiler picks the Currency-to-uint-to-ulong route in preference to Currency-to-float-to-ulong.)

To test the SimpleCurrency2 sample, add this code to the test code for SimpleCurrency:

```
try
{
    Currency balance = new Currency(50,35);
    Console.WriteLine(balance);
    Console.WriteLine("balance is " + balance);
    Console.WriteLine("balance is (using ToString()) " + balance.ToString());
    uint balance3 = (uint) balance;
    Console.WriteLine("Converting to uint gives " + balance3);
}
```

code snippet SimpleCurrency2/Program.cs

Running the sample now gives you these results:

# SIMPLECURRENCY2

```
50
balance is $50.35
balance is (using ToString()) $50.35
Converting to uint gives 50
After converting to float, = 50.35
After converting back to Currency, = $50.34
Now attempt to convert out of range value of -$50.50 to a Currency:
Result is $4294967246.00
```

The output shows that the conversion to uint has been successful, though as you have lost the cents part of the Currency in making this conversion. Casting a negative float to Currency has also produced the expected overflow exception now that the float-to-Currency cast itself defines a checked context.

However, the output also demonstrates one last potential problem that you need to be aware of when working with casts. The very first line of output has not displayed the balance correctly, displaying 50 instead of $50.35. Consider these lines:

```
Console.WriteLine(balance);
Console.WriteLine("balance is " + balance);
Console.WriteLine("balance is (using ToString()) " + balance.ToString());
```

Only the last two lines correctly display the Currency as a string. So what is going on? The problem here is that when you combine casts with method overloads, you get another source of unpredictability. We will look at these lines in reverse order.

The third Console.WriteLine() statement explicitly calls the Currency.ToString() method, ensuring that the Currency is displayed as a string. The second does not do so. However, the string literal "balance is" passed to Console.WriteLine() makes it clear to the compiler that the parameter is to be interpreted as a string. Hence, the Currency.ToString() method will be called implicitly.

The very first Console.WriteLine() method, however, simply passes a raw Currency struct to Console.WriteLine(). Now, Console.WriteLine() has many overloads, but none of them takes a Currency struct. So the compiler will start fishing around to see what it can cast the Currency to in order to make it match up with one of the overloads of Console.WriteLine(). As it happens, one of the Console.WriteLine() overloads is designed to display uints quickly and efficiently, and it takes a uint as a parameter — you have now supplied a cast that converts Currency implicitly to uint.