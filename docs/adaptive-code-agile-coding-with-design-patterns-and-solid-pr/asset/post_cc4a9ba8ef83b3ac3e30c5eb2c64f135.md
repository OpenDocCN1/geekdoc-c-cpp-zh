
As shown in Listing 6-16, the Account class is no longer abstract and therefore no longer requires the Base suffix. For construction, it accepts an IRewardCard instance and delegates to this when adding a transaction. Overall, this account looks more like it used to before the initial requirement for capturing reward points.

### LISTING 6-16 Each account contains a reward card.

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

## Aggressive refactoring

Code is never done. Code can be working, good enough, sufficient, valuable, and producing revenue. But it is rarely, if ever, complete. Often, code is found in a certain state, but it is only a snapshot of a transitioning form. Code is always on a journey from where it is now to some unknown place in the future. When code is considered finished, there is the temptation to label it pejoratively. It becomes "stupid," "unreadable"—a figure of ridicule. Worse still, you might start to consider its authors as stupid or bad coders, or even malevolent forces, spitefully making your life a waking nightmare.

If you instead consider code as perpetually unfinished, you are better able to break the inertia to change. No code is ever sacred. Code can be underdeveloped and in need of some engineering discipline, or overwrought and in need of simplification. Different parts of the code might exhibit each property, perhaps in startling proximity. Never be afraid to roll your sleeves up and set about *improving* something. Even if you revert your changes, you will learn something, guaranteed. Better still, use your skills as an adaptive code ninja to aggressively refactor it into a better shape.

Aggressive refactoring is what normal refactoring should be but rarely is. Refactoring should be continuous and diligent. It should also occur at different scopes. The refactorings discussed so far in this chapter are somewhat tactical. This is fine, but it will result in code that is clean at the lowest levels but that lacks a discernible structure. Capturing magic numbers in constant variables is a noble undertaking, but it will not result in code that can absorb the functionality of endless new requirements.

For this, a new phase is needed in the development process: *redesign.*

## Red, green, refactor...redesign

Refactoring implies the fourth conceptual stage, *redesign*, but developers often stop short of refactoring so much. There are also nuanced differences in the rules for refactoring versus redesigning.

When you are refactoring, the unit tests protect against a misstep by specifying the expected behavior of the code. If the refactor goes wrong and you inadvertently change the behavior of the code in addition to its design, the unit test fails. Recovery is simple: revert the changes and try again.

When you are redesigning, the unit tests will no longer apply as valid tests of the design. Changing the name of a production class or method, either manually or by automated tools, is a refactor, not a redesign. Replacing that class with an entirely new class, whose methods accept different parameters and return different outputs, is a redesign. The difference is that the unit tests must change in order to be effective.

The steps for redesigning, and therefore aggressive refactoring, are twofold. First, the tests must change first to reflect the new design. Second, the production code to satisfy the new design must be created in parallel.

Changing the tests first ensures that you are still doing test-first development (not to be confused with test-driven design; see Chapter 5). Implementing the new production code in parallel ensures that you do not break the existing code for any length of time. Try to avoid committing code that is broken to source control. If the code was broken at any time during the redesign, it could not be committed to source control. This would put you in the awkward situation of needing to redesign code all in one sitting without any pauses or breaks. This is not enforceable, because the work of a developer is fraught with constant interruptions and context switches.

## Making legacy code adaptive

> Legacy code is code without tests.
>
> — Michael Feathers, *Working Effectively with Legacy Code*

All examples of refactoring up to this point have assumed that the code that is the target of your refactors has sufficient tests to protect against a refactoring mistake. What if there are no unit tests?

In his great book, *Working Effectively with Legacy Code* (Prentice Hall, 2014), Michael Feathers asserts that legacy code is not simply code from a bygone era written in Cobol or some such arcane language. No, the differentiating factor that distinguishes legacy code is that it does not have any unit tests that verify its behavior.

Such code makes refactoring more difficult, because there is no guarantee against an inevitable mistake that could alter the behavior and the structure of the code. Furthermore, the omission of tests also correlates with poor code design, so legacy code is both perilous to refactor and in desperate need of refactoring! This lack of design is what makes it so difficult to retrofit unit tests so that the code can be safely refactored.

## The golden master technique

Michael Feathers solves this problem with two types of tests: characterization tests and a golden master.

Characterization tests are intended to capture the current behavior of the system. The goal is not to be exhaustive, mapping the range of all possible inputs to the domain of all possible outputs. Instead, the goal is to capture the general ebb and flow of the code’s runtime execution.

When the characterization tests have been created, the system’s current behavior is stored, perhaps as log messages in a file. This file is now your expectation for the system, and the output of the characterization tests is disabled. These expectations can form the basis of test assertions. The golden master will run the system and capture a current view of the characterization tests. From here, changes can be made to the system, and the output of the characterization tests compared against the golden master. Any deviation from the expected paths will result in a test failure. With a green, passing test, you have given yourself some confidence that your refactoring efforts have not altered the behavior of the legacy code.

Only when the expected behavior of the system has changed do you regenerate the golden master by re-running the characterization tests. During the normal course of regression testing, the generation of the golden master is disabled, but the assertion of current behavior versus expected behavior remains enabled.

Of course, this technique lacks the precision of true unit tests, but the idea is that each refactor is more of a redesign. This will generate a parallel design that is implemented by using a test-first process. As the suite of unit tests grows, so does your confidence that the application is still functional.

## The trade processor

Listing 6-17 shows a class called TradeProcessor that you want to refactor. This code is *legacy code*, by the Michael Feathers definition: it does not have any accompanying tests.

### LISTING 6-17 Changing code without tests is perilous without first introducing some tests.

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

        var trades = new List<TradeRecord>();

        var lineCount = 1;
        foreach(var line in lines)
        {
            var fields = line.Split(new char[] { ',' });

            if(fields.Length != 3)
            {
                Console.WriteLine("WARN: Line {0} malformed. Only {1} field(s) found.",
lineCount, fields.Length);
                continue;
            }

            if(fields[0].Length != 6)
            {
                Console.WriteLine("WARN: Trade currencies on line {0} malformed: '{1}'",
lineCount, fields[0]);
                continue;
            }

            int tradeAmount;
            if(!int.TryParse(fields[1], out tradeAmount))
            {
                Console.WriteLine("WARN: Trade amount on line {0} not a valid integer: '{1}'", lineCount, fields[1]);
            }

            decimal tradePrice;
            if (!decimal.TryParse(fields[2], out tradePrice))
```
