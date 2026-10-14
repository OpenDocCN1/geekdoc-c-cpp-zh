
The number of reward points earned is dependent on multiple factors, which complicate the calculation method:

- The account type—more points are earned at higher tiers.
- The amount of the transaction—the more customers spend, the more points they earn.
- The current balance of the account—the Gold and Platinum tiers give customers more points for keeping their balance high.

Assuming that this code has been written alongside its unit tests, those tests will help greatly by ensuring that changes do not affect the specified behavior. This is an important point—refactoring changes the arrangement of the code, not the outcome. If you tried to refactor without unit tests, how would you know if you inadvertently broke the expected behavior? You would not fail fast but much later at run time during testing or, worse, after deployment.

## Replacing “magic numbers” with constants

The first refactor is a simple but nonetheless important improvement to the readability of the code. There are a lot of “magic numbers” littering the CalculateRewardPoints method. Six distinct numbers are used without any context as to what they mean or why they are required. To the person who wrote the code, their significance might be obvious because that person has prior knowledge of what it all means. In reality, that will probably only be true for a week, perhaps two, before the person’s memory starts to fade and he loses track of what that 5, or that 2, means. Listing 4-29 shows the changes made to the class as a result of this refactor.

## LISTING 4-29 This code is more readable to people unfamiliar with it.

Click here to view code image

```
public class Account
{
    public int CalculateRewardPoints(decimal amount)
    {
        int points;
        switch(type)
        {
            case AccountType.Silver:
                points = (int)decimal.Floor(amount / SilverTransactionCostPerPoint);
                break;
            case AccountType.Gold:
                points = (int)decimal.Floor((Balance / GoldBalanceCostPerPoint) + (amount / GoldTransactionCostPerPoint));
                break;
            case AccountType.Platinum:
                points = (int)decimal.Ceiling((Balance / PlatinumBalanceCostPerPoint) + (amount / PlatinumTransactionCostPerPoint));
                break;
            default:
```

```
points = 0;
    break;
}
    return Math.Max(points, 0);
}

private const int SilverTransactionCostPerPoint = 10;
private const int GoldTransactionCostPerPoint = 5;
private const int PlatinumTransactionCostPerPoint = 2;

private const int GoldBalanceCostPerPoint = 2000;
private const int PlatinumBalanceCostPerPoint = 1000;
}
```

Each of the “magic numbers” has been replaced with an equivalent variable. There is a set of three variables for the cost-per-point denominator of the transaction amount, one per account type. Then there are two variables for the cost-per-point denominator of the balance amount, for the Gold and Platinum account types, which are the only two account types that offer this incentive.

The benefit of this refactor is that the code is now understandable to people who are unfamiliar with it, because you have explained what the values mean through the variable names. It would not be an improvement if you merely replaced the “magic numbers” with variables named A, B, or X. Try to choose variable names that explain concisely their purpose. Never be afraid of verbosity, and take every opportunity to self-document code through variable, class, and method names.

## Replacing a conditional expression with polymorphism

The next refactor is more involved. The switch statement, which alters the CalculateRewards algorithm depending on the account type, is problematic for two reasons. First, it adversely affects readability but, more pressingly, it introduces a maintenance burden. Imagine that you are given a new requirement at some time in the future: a new account type. It has been decided that not enough people are meeting the criteria for the Silver account, so you need to create a new Bronze account. To add the Bronze account, you would need to edit the Account class and add tests to it. Editing existing code in this way, after it has been verified and deployed, should be avoided. Instead, you should look to other ways that you can extend code so that it is adaptable without being editable.

What you are aiming to achieve is to make it easier to add a new account type while improving the readability of the code. For this, you will take advantage of polymorphism. You will model the account types as different subclasses of the Account class. The Gold account type will be represented by the GoldAccount class, and the same is true of the SilverAccount and PlatinumAccount.

The first step is to define these classes, as shown in Listing 4-30.

## LISTING 4-30 Each account type is now a distinct class.

Click here to view code image

```
public class SilverAccount
```

```
{
    public int CalculateRewardPoints(decimal amount)
    {
        return Math.Max((int)decimal.Floor(amount / SilverTransactionCostPerPoint), 0);
    }

    private const int SilverTransactionCostPerPoint = 10;
}
// ...
public class GoldAccount
{
    public decimal Balance
    {
        get;
        set;
    }

    public int CalculateRewardPoints(decimal amount)
    {
        return Math.Max((int)decimal.Floor((Balance / GoldBalanceCostPerPoint) + (amount / GoldTransactionCostPerPoint)), 0);
    }

    private const int GoldTransactionCostPerPoint = 5;
    private const int GoldBalanceCostPerPoint = 2000;
}
// ...
public class PlatinumAccount
{
    public decimal Balance
    {
        get;
        set;
    }

    public int CalculateRewardPoints(decimal amount)
    {
        return Math.Max((int)decimal.Ceiling((Balance / PlatinumBalanceCostPerPoint) + (amount / PlatinumTransactionCostPerPoint)), 0);
    }

    private const int PlatinumTransactionCostPerPoint = 2;
    private const int PlatinumBalanceCostPerPoint = 1000;
}
```

Note that, at this stage, the original Account class has not been changed. These classes have been created as stand-alone classes. The unit tests for these classes would mirror the expectations of the CalculateRewardPoints class, but with a different SUT for each account type. The algorithms for determining the reward points due on the Platinum and Gold classes have a dependency on the current balance; that has been included so that these classes compile in isolation. The Balance property is also publically settable, which enables unit testing with different values. The UML class diagram in Figure 4-8 explains how these classes are related.

![](img/65c1bad7a6b3cffae8cbb79664f0708b_179_0.png)

FIGURE 4-8 The Account class will become abstract with an abstract CalculateRewardPoints method.

This is merely an objective on the way to completing the goal of replacing the switch statement, of course. It is important not to do too much all at once, so that you can verify that you are on the right track with a succession of smaller changes. The next change, in Listing 4-31, is to link all four classes into an inheritance hierarchy.

## LISTING 4-31 The complexity has been removed from the Account class.

Click here to view code image

```
public abstract class AccountBase
{
    public decimal Balance
    {
        get;
        private set;
    }

    public int RewardPoints
```

```
{
    get;
    private set;
}

public void AddTransaction(decimal amount)
{
    RewardPoints += CalculateRewardPoints(amount);
    Balance += amount;
}

public abstract int CalculateRewardPoints(decimal amount);
}
```

Without the switch statement, there is no reason for this class to be aware of its “type” anymore, so the constructor has been removed, too. The class is abstract due to the abstract calculation method, but this means that you can no longer instantiate it and, consequently, you can no longer test it.

An object instance is needed for the unit tests to work, so the next step is to link the three account types as subclasses of this base. A useful naming convention—along with prefixing interface names with a capital I—is to suffix abstract classes with Base. This a quick clue that the class cannot be instantiated and has associated subclasses.

When the three subclasses are created, you can remove the Balance property from the Gold-Account and PlatinumAccount because they will inherit the Balance and AddTransaction members from this base. Listing 4-32 shows all three classes after this step.

## LISTING 4-32 Completing the refactor by inheriting from the base class.

Click here to view code image

```
public class SilverAccount : AccountBase
{
    public override int CalculateRewardPoints(decimal amount)
    {
        return Math.Max((int)decimal.Floor(amount / SilverTransactionCostPerPoint), 0);
    }

    private const int SilverTransactionCostPerPoint = 10;
}
// ...
public class GoldAccount : AccountBase
{
    public override int CalculateRewardPoints(decimal amount)
    {
        return Math.Max((int)decimal.Floor((Balance / GoldBalanceCostPerPoint) + (amount /
```
