```
~~~csharp
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
~~~
```