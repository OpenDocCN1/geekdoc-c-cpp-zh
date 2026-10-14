
## Replacing inheritance with delegation

In practice, this means that you need to split the AccountBase class into two parts. Some of the interface will remain on the account, with some of it moving to a new class hierarchy to represent reward cards. In this way, the inheritance of accounts is replaced with delegation to reward cards.

The first change is to introduce a new IRewardCard interface to define the properties and behavior of each reward card, as shown in Listing 4-41.

### LISTING 4-41 The reward points and their calculation have moved away from the Account class.

Click here to view code image

```
public interface IRewardCard
{
    int RewardPoints
    {
        get;
    }

    void CalculateRewardPoints(decimal transactionAmount, decimal accountBalance);
}
```

Previously, these two members were part of the AccountBase class, but they have been moved out because they are wholly dependent on the presence of reward cards. Note that the interface of CalculateRewardPoints has changed in two ways. First, there is no longer a return value on this method, because it is expected to mutate the RewardPoints property directly. Second, you must pass in the account balance as a parameter to this method because it is no longer available. This is an important side effect of splitting the two objects up in this manner: any context not directly encapsulated by the reward card object will need to be handed to it. This might cause the interface of this method to change in the future.

Listing 4-42 shows the implementations of this interface for the Bronze and Platinum cards after the refactor.

### LISTING 4-42 Examples of the reward card implementations.

Click here to view code image

```
internal class BronzeRewardCard : IRewardCard
{
    public int RewardPoints
    {
        get;
        private set;
    }

    public void CalculateRewardPoints(decimal transactionAmount, decimal accountBalance)
    {
        RewardPoints += Math.Max((int)decimal.Floor(transactionAmount / BronzeTransactionCostPerPoint), 0);
    }
    private const int BronzeTransactionCostPerPoint = 20;
}
//...
internal class PlatinumRewardCard : IRewardCard
{
    public int RewardPoints
    {
        get;
        private set;
    }

    public void CalculateRewardPoints(decimal transactionAmount, decimal accountBalance)
    {
        RewardPoints += Math.Max((int)decimal.Ceiling((accountBalance / PlatinumBalanceCostPerPoint) + (transactionAmount / PlatinumTransactionCostPerPoint)), 0);
    }

    private const int PlatinumTransactionCostPerPoint = 2;
    private const int PlatinumBalanceCostPerPoint = 1000;
}
```

These classes are very similar to their previous incarnation, with an extra local RewardPoints property.

As shown in Listing 4-43, the Account class is no longer abstract and therefore no longer requires the Base suffix. For construction, it accepts an IRewardCard instance and delegates to this when adding a transaction. Overall, this account looks more like it used to before the initial requirement for capturing reward points.

### LISTING 4-43 Each account contains a reward card.

Click here to view code image

```
public class Account
{
    public Account(IRewardCard rewardCard)
    {
        this.rewardCard = rewardCard;
    }

    public decimal Balance
    {
        get;
        private set;
    }

    public void AddTransaction(decimal amount)
    {
        rewardCard.CalculateRewardPoints(amount, Balance);
        Balance += amount;
    }

    private readonly IRewardCard rewardCard;
}
```

To model a Standard account—an account without a reward card—you can either pass in null for the reward card constructor dependency (and protect against a NullReferenceException by testing for null before delegating) or you can model a NullRewardCard. The latter would be an implementation of the Null Object pattern that would not accumulate any reward points when CalculateRewardPoints was called.

## Conclusion

This chapter has been a hybrid of unit testing and refactoring because the two should be paired together and performed in tandem.

Each unit test you write should represent an expectation of the code that, ideally, should be communicable to a layperson. Although as code they are technical artifacts, unit tests enforce real-world behavior in objects, just as those objects encapsulate real-world concepts.

When you diligently follow a test-first approach, you write no new production code without first constructing a failing unit test. Then you write the simplest production code possible to transition the unit test from a red failure state to a green success state. Taken to its logical conclusion, the production code becomes a natural side effect of fulfilling the expectations of its unit tests.

When you unit test code, you give yourself a firm foundation to subsequently alter the production code to make it clearly more adaptive to future requirements. The refactoring of code is an incremental process of improving the code’s design. There are many options for refactoring, only some of which were explored in this chapter. Each option available might represent a tradeoff in one area for a certain improvement in another, and—as with many aspects of programming—the process is quite subjective.

With this chapter complete, the Agile foundation part of this book is closed. Next you will look at SOLID code and how it will help to further increase the adaptability of your code.

## Part II: Writing SOLID code

- CHAPTER 5 The single responsibility principle
- CHAPTER 6 The open/closed principle
- CHAPTER 7 The Liskov substitution principle
- CHAPTER 8 Interface segregation
- CHAPTER 9 Dependency injection

*SOLID* is the acronym for a set of practices that, when implemented together, make code adaptive to change. The SOLID practices were introduced by Bob Martin almost 15 years ago. Even so, these practices are not as widely known as they could be—and perhaps should be.

In this part, a chapter is devoted to each of the SOLID principles:

- S The single responsibility principle
- O The open/closed principle
- L The Liskov substitution principle
- I Interface segregation
- D Dependency injection

Even taken in isolation, each of these principles is a worthy practice that any software developer would do well to learn. When used in collaboration, these patterns give code a completely different structure—one that lends itself to change.

However, take note that these patterns and practices, just like all others, are merely tools for you to use. Deciding when and where to apply any pattern or practice is part of the art of software development. Overuse leads to code that is adaptive, but on too fine-grained a level to be appreciated or useful. Overuse also affects another key facet of code quality: readability. It is far more common for software to be developed in teams than as an individual pursuit. Thus, judiciously selecting when and where to apply each pattern, practice, or SOLID principle is imperative to ensure that the code remains comprehensible in the future.

## Chapter 5. The single responsibility principle

### After completing this chapter, you will be able to

- Understand the importance of the single responsibility principle.
- Identify classes that have too many responsibilities.
- Write modules, classes, and methods that have a single responsibility.
- Refactor monolithic classes into smaller classes with single responsibilities.
- Use design patterns to separate responsibilities.

The single responsibility principle (SRP) instructs developers to write code that has one and only one reason to change. If a class has more than one reason to change, it has more than one responsibility. Classes with more than a single responsibility should be broken down into smaller classes, each of which should have only one responsibility and reason to change.

This chapter explains that process and shows you how to create classes that only have a single responsibility but are still useful. Through a process of delegation and abstraction, a class that contains too many reasons to change should delegate one or more responsibilities to other classes.

It is difficult to overstate the importance of delegating to abstractions. It is the lynchpin of adaptive code and, without it, developers would struggle to adapt to changing requirements in the way that Scrum and other Agile processes demand.

## Problem statement

To better explain the problem with having classes that hold too many responsibilities, this section explores an example. Listing 5-1 shows a simple batch processor class that reads records from a file and updates a database. Despite its small size, you need to continually add features to this batch processor so that it meets the needs of your business.

### LISTING 5-1 An example of a class with too many responsibilities.

Click here to view code image

```
public class TradeProcessor
{
    public void ProcessTrades(System.IO.Stream stream)
    {
        // read rows
        var lines = new List<string>();
        using(var reader = new System.IO.StreamReader(stream))
        {
            string line;
            while((line = reader.ReadLine()) != null)
            {
                lines.Add(line);
            }
        }
```
