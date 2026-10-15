# Using a Method with Parameters

Parameters provide a means of passing values to a method. In C#, you can pass a parameter to a method in four different ways: by value, using the ref keyword, using the out keyword, and using the params keyword. A parameter declared without any modifier is a value parameter. Now, create a new Console application, named MyMethodParameters (also available in the CD). Replace the default code of the Program.cs file of the application with the code shown in Listing 4.8:

# Listing 4.8: Showing the Code of the MyMethodParameters Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MyMethodParameters
{
    class Program
    {
        static void Main(string[] args)
        {
            Amount Amt = new Amount();
            Amt.Balance(12000, 2000);
            Amt.GetData();
            Console.Write("\nPress ENTER to quit..");
            Console.ReadLine();
        }
    }
    public class Amount
    {
        double BalanceAmount;
        public void Balance(double TotalAmount, double Deductions)
        {
            BalanceAmount = TotalAmount - Deductions;
            Console.WriteLine("Your Current Amount is Rs: " + BalanceAmount);
        }
        public void Debit()
        {
            int DebitAmount = 0;
            Console.Write("Enter Amount:");
            DebitAmount = int.Parse(Console.ReadLine());
            BalanceAmount = BalanceAmount - DebitAmount;
            Console.WriteLine("Your Balance Amount is Rs.:" + BalanceAmount);
        }
        public void Credit()
        {
            int CreditAmount = 0;
            Console.Write("Enter Amount:");
            CreditAmount = int.Parse(Console.ReadLine());
            BalanceAmount = BalanceAmount + CreditAmount;
            Console.WriteLine("Your Balance Amount is Rs.:" + BalanceAmount);
        }
        public void GetData()
        {
            char Data;
            Console.WriteLine("----------------------------------------");
            Console.Write("Press (d) for Debit and (c) for Credit:");
            Data = char.Parse(Console.ReadLine());
```