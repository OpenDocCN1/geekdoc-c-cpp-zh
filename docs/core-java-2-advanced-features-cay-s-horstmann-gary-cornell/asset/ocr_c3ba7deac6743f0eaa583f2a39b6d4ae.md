# Listing 7.5 *(Continued)*

```
```java
info.setInflationPercent(
    percentFmt.parse(inflationField.getText()).doubleValue());
}
catch (ParseException ex)
{
    ex.printStackTrace();
}
}

/**
 * The information required to compute retirement income data.
 */
class RetireInfo
{
    private double savings;
    private double contrib;
    private double income;
    private int currentAge;
    private int retireAge;
    private int deathAge;
    private double inflationPercent;
    private double investPercent;
    private int age;
    private double balance;

    /**
     * Gets the available balance for a given year.
     * @param year the year for which to compute the balance
     * @return the amount of money available (or required) in that year
     */
    public double getBalance(int year)
    {
        if (year < currentAge) return 0;
        else if (year == currentAge)
        {
            age = year;
            balance = savings;
            return balance;
        }
        else if (year == age) return balance;
        if (year != age + 1) getBalance(year - 1);
        age = year;
        if (age < retireAge) balance += contrib;
        else balance -= income;
        balance = balance * (1 + (investPercent - inflationPercent));
        return balance;
    }
```

```