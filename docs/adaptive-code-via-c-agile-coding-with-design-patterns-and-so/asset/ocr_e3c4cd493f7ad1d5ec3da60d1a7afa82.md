```
get;
private set;
}

public int RewardPoints
{
    get;
    private set;
}

public void AddTransaction(decimal amount)
{
    RewardPoints += CalculateRewardPoints(amount);
    Balance += amount;
}

public int CalculateRewardPoints(decimal amount)
{
    int points;
    switch(type)
    {
        case AccountType.Silver:
            points = (int)decimal.Floor(amount / 10);
            break;
        case AccountType.Gold:
            points = (int)decimal.Floor((Balance / 10000 * 5) + (amount / 5));
            break;
        case AccountType.Platinum:
            points = (int)decimal.Ceiling((Balance / 10000 * 10) + (amount / 2));
            break;
        default:
            points = 0;
            break;
    }
    return Math.Max(points, 0);
}

private readonly AccountType type;
}
```

The most important changes to the class are summarized thus:

+   - A new property tracks the number of reward points that the customer has linked to this account.
+   - Each account has a type code that indicates the tier of the account: Silver, Gold, or Platinum.
+   - Whenever a transaction is added to the account, the customer earns reward points.