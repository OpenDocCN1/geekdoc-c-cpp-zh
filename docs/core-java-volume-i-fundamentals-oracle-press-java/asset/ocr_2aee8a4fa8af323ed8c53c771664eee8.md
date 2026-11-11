amount currently accumulated in the body of the loop until the total exceeds the targeted amount.

```
```java
while (balance < goal)
{
    balance += payment;
    double interest = balance * interestRate / 100;
    balance += interest;
    years++;
}
System.out.println(years + " years.");
```
```

(Don’t rely on this program to plan for your retirement. It lacks a few niceties such as inflation and your life expectancy.)

A while loop tests at the top. Therefore, the code in the block might never be executed. If you want to make sure a block is executed at least once, you need to move the test to the bottom, using the do/while loop. Its syntax looks like this:

do *statement* while *(condition)*;

This loop executes the statement (which is typically a block) and only then tests the condition. If it’s true, it repeats the statement and retests the condition, and so on. The code in Listing 3.4 computes the new balance in your retirement account and then asks if you are ready to retire:

```
```java
do
{
    balance += payment;
    double interest = balance * interestRate / 100;
    balance += interest;
    years++;
    // print current balance
    . . .
    // ask if ready to retire and get input
    . . .
```
```