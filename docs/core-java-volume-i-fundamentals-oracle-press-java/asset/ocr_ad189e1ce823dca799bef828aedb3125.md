See if you can spot the problems with the code in [Listing 12.3](#) and the Bank class in [Listing 12.2](#). We will unravel the mystery in the next section.

# Listing 12.3 unsynch/UnsynchBankTest.java

```
```java
 1 package unsynch;
 2 
 3 /**
 4  * This program shows data corruption when multiple threads
 access a data structure.
 5  * @version 1.32 2018-04-10
 6  * @author Cay Horstmann
 7  */
 8 public class UnsynchBankTest
 9 {
10     public static final int NACCOUNTS = 100;
11     public static final double INITIAL_BALANCE = 1000;
12     public static final double MAX_AMOUNT = 1000;
13     public static final int DELAY = 10;
14 
15     public static void main(String[] args)
16     {
17         var bank = new Bank(NACCOUNTS, INITIAL_BALANCE);
18         for (int i = 0; i < NACCOUNTS; i++)
19         {
20             int fromAccount = i;
21             Runnable r = () ->
22                 {
23                     try
24                     {
25                         while (true)
26                         {
27                             int toAccount = (int) (bank.size() *
 Math.random());
28                             double amount = MAX_AMOUNT *
 Math.random();
29                             bank.transfer(fromAccount, toAccount,
 amount);
30                             Thread.sleep((int) (DELAY *
 Math.random()));
```
```