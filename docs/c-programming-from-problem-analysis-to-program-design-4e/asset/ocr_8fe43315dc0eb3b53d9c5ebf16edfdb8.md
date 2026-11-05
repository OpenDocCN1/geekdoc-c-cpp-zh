```
DetermineTotalInterestPaid()
set totalInterestPaid = 0
set balance = loanAmount
set month = 1
loop while (month <= numPayments)
  CalculateMonthCharges(month, numPayments)
  totalInterestPaid = totalInterestPaid + monthInterest
  month = month + 1
}
```

```
string : ReturnAmortizationSchedule()
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
principal = payment – monthInterest
balance = balance - principal
```

```
DeterminePaymentAmount()
set term = Math.Pow(1 + rate / 12), numPayments)
set paymentAmount = (loanAmount * rate / 12 * term) / (term – 1.0)
```

# FIGURE 6-19 Behavior of Loan class methods

Loan Class