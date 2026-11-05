
## 图 6-19 Loan 类方法的行为

### Loan 类

```
DetermineTotalInterestPaid()
set totalInterestPaid = 0
set balance = loanAmount
set month = 1
loop while (month <= numPayments)
{
  CalculateMonthCharges(month, numPayments)
  totalInterestPaid = totalInterestPaid + monthInterest
  month = month + 1
}
```

```
string ReturnAmortizationSchedule()
set aSchedule = --- heading for columns ---
balance = loanAmount
month = 1
loop while (month <= numPayments)
{
CalculateMonthCharges(month, numPayments)
set aSchedule += month + monthInterest + principal + balance + "\n"
month = month + 1
}
return aSchedule
```

```
CalculateMonthCharges(int month, int numPayments)
set payment = paymentAmount
set monthInterest = rate / 12 * balance
if (month == numPayments)
{
set principal = balance
set payment = balance + monthInterest
}
else
  principal = payment - monthInterest
balance = balance - principal
```

```
DeterminePaymentAmount()
set term = Math.Pow((1 + rate / 12), numPayments)
set paymentAmount = (loanAmount * rate / 12 * term) / (term - 1.0)
```

![](img/36e48639a06772bcb0fa1ea2525b33a3_402_0.png)

算法开发完成后，应检查设计的正确性。在以往的应用中，你可以使用标准计算器，并将程序产生的结果与计算器产生的值进行比较。有时你需要额外资源来验证输出的正确性。在互联网上，你可以找到分期偿还表，也可以使用金融计算器来测试结果。表 6-6 包含可用于验证编程示例正确性的值。

**表 6-6** LoanApp 测试值

| 贷款金额 | 利率 | 年限 | 还款额 | 总利息 |
|---:|---:|---:|---:|---:|
| 50000 | .08 | 10 | 606.64 | 22,796.56 |
| 22000 | .05 | 5 | 415.17 | 2,910.03 |
| 150000 | .055 | 30 | 851.68 | 156,606.06 |
| 12000 | .06 | 3 | 365.06 | 1,142.28 |
| 10000 | .05 | 2 | 438.71 | 529.13 |

## 编写解决方案代码

实现设计后，你可以将这些结果与从程序输出中获得的结果进行比较。这有时称为桌面检查（desk run）。

完成设计并验证算法的正确性后，就该将设计转换为源代码了。对于此应用程序，你将创建两个单独的文件——每个类一个文件。两个文件的最终应用程序清单如下：

```csharp
/* Loan.cs
 * Creates fields for the amount of loan, interest
 * rate, and number of years. Calculates amount of payment
 * and produces an amortization schedule.
 */
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
namespace LoanApp
{
    public class Loan
    {
        private double loanAmount;
        private double rate;
        private int numPayments;
        private double balance;
        private double totalInterestPaid;
        private double paymentAmount;
        private double principal;
        private double monthInterest;

        // Default constructor
        public Loan()
        {
        }

        // Constructor
        public Loan(double loan, double interestRate, int years)
        {
            loanAmount = loan;
            if (interestRate < 1)
                rate = interestRate;
            else //In case directions aren't followed
                rate = interestRate / 100; // convert to decimal.
            numPayments = 12 * years;
            totalInterestPaid = 0;
            DeterminePaymentAmount();
        }

        // Property accessing payment amount
        public double PaymentAmount
        {
            get
            {
                return paymentAmount;
            }
        }

        // Property setting and returning loan amount
        public double LoanAmount
        {
            set
            {
                loanAmount = value;
            }
            get
            {
                return loanAmount;
            }
        }

        // Property setting and returning rate
        public double Rate
        {
            set
            {
                rate = value;
            }
            get
            {
                return rate;
            }
        }

        // Property to set the numPayments, given years to finance.
        // Returns the number of years using number of payments.
        public int Years
        {
            set
            {
                numPayments = value * 12;
            }
            get
            {
                return numPayments / 12;
            }
        }

        // Property for accessing total interest to be paid
        public double TotalInterestPaid
        {
            get
            {
                return totalInterestPaid;
            }
        }

        // Determine payment amount based on number of years,
        // loan amount, and rate.
        public void DeterminePaymentAmount()
        {
            double term;
            term = Math.Pow((1 + rate / 12.0), numPayments);
            paymentAmount = (loanAmount * rate / 12.0 * term)
                            / (term - 1.0);
        }

        // Returns a string containing an amortization table.
        public string ReturnAmortizationSchedule()
        {
            string aSchedule = "Month\t\tInt.\t\tPrin.\t\tNew";
            aSchedule += "\nNo.\t\tPd.\t\tPd.\t\tBalance\n";
            aSchedule += "------\t------\t------\t--------\n";
            balance = loanAmount;
            for (int month = 1; month <= numPayments; month++)
            {
                CalculateMonthCharges(month, numPayments);
                aSchedule += month
                    + "\t"
                    + monthInterest.ToString("N2")
                    + "\t"
                    + principal.ToString("N2")
                    + "\t"
                    + balance.ToString("C")
                    + "\n";
            }
            return aSchedule;
        }

        // Calculates monthly interest and new balance.
        public void CalculateMonthCharges(int month,
                                           int numPayments)
        {
            double payment = paymentAmount;
            monthInterest = rate / 12 * balance;
            if (month == numPayments)
            {
                principal = balance;
                payment = balance + monthInterest;
            }
            else
            {
                principal = payment - monthInterest;
            }
            balance -= principal;
        }

        // Calculates interest paid over the life of the loan.
        public void DetermineTotalInterestPaid()
        {
            totalInterestPaid = 0;
            balance = loanAmount;
            for (int month = 1; month <= numPayments; month++)
            {
                CalculateMonthCharges(month, numPayments);
                totalInterestPaid += monthInterest;
            }
        }

        // Return information about the loan
        public override string ToString()
        {
            return "\nLoan Amount: " + loanAmount.ToString("C") +
                   "\nInterest Rate: " + rate +
                   "\nNumber of Years for Loan: " +
                   (numPayments / 12) +
                   "\nMonthly payment: " +
                   paymentAmount.ToString("C");
        }
    }
}
```

```csharp
/* LoanApp.cs
 * Used for testing Loan class.
 * Prompts user for loan amount,
 * interest rate, and time period
 * for loan. Calls method to display
 * payment amount and amortization
 * schedule. Allows more than
 * one loan calculation.
 */

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
namespace LoanApp
{
    class LoanApp
    {
        static void Main()
        {
            int years;
            double loanAmount;
            double interestRate;
            string inValue;
            char anotherLoan = 'N';

            do
            {
                GetInputValues(out loanAmount,
                               out interestRate, out years);

                Loan ln = new
                    Loan(loanAmount, interestRate, years);
                Console.WriteLine();

                Console.Clear();
                Console.WriteLine(ln);
                Console.WriteLine();

                Console.WriteLine(ln.ReturnAmortizationSchedule());
                Console.WriteLine("Payment Amount: {0:C}",
                    ln.PaymentAmount);
                Console.WriteLine("Interest Paid over Life " +
                    "of Loan: {0:C}",
                    ln.TotalInterestPaid);
                Console.Write("Do another Calculation? (Y or N)");
                inValue = Console.ReadLine();
                anotherLoan = Convert.ToChar(inValue);
            }
            while ((anotherLoan == 'Y') || (anotherLoan == 'y'));
        }

        // Prompts user for loan data
        public static void GetInputValues(out double loanAmount,
                                          out double interestRate,
                                          out int years)
        {
            Console.Clear();
            loanAmount = GetLoanAmount();
            interestRate = GetInterestRate();
            years = GetYears();
        }

        public static double GetLoanAmount()
        {
            string sValue;
            double loanAmount;

            Console.Write("Please enter the loan amount: ");
            sValue = Console.ReadLine();
            while (double.TryParse(sValue, out loanAmount) == false)
            {
                Console.WriteLine("Invalid data entered " +
                    "for loan amount");
                Console.Write("\nPlease re-enter the loan amount: ");
                sValue = Console.ReadLine();
            }
            return loanAmount;
        }
    }
}
```
