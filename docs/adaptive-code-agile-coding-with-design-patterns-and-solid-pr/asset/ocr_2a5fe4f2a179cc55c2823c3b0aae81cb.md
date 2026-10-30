Note that, at this stage, the original Account class has not been changed. These classes have been created as standalone classes. The unit tests for these classes would mirror the expectations of the CalculateRewardPoints class, but with a different system under test (SUT) for each account type. The algorithms for determining the reward points due on the Platinum and Gold account classes have a dependency on the current balance; that has been included so that these classes compile in isolation. The Balance property is also publicly settable, which enables unit testing with different values. The UML class diagram in Figure 6-1 explains how these classes are related.

![](bbox=[0.1, 0.35, 0.9, 0.62])

FIGURE 6-1 The Account class will become abstract with an abstract CalculateRewardPoints method.

This is merely an objective on the way to completing the goal of replacing the switch statement, of course. It is important not to do too much all at once, so that you can verify that you are on the right track with a succession of smaller changes. The next change, in Listing 6-4, is to link all four classes into an inheritance hierarchy.

# LISTING 6-4 The complexity has been removed from the Account class.

```
public abstract class AccountBase
{
    public decimal Balance
    {
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

    public abstract int CalculateRewardPoints(decimal amount);
}
```