Within the loop, the next balance is calculated, and the user is prompted for a response. The Boolean expression that controls loop execution is written using a while statement, placed after the loop body. The bankBal variable is output the first time before the user has any option of responding. At the end of the loop, the user is prompted, Do you want to see next year's balance? Y or N.... Now the user has the option of seeing more balances, but the first view of the balance was unavoidable.

![](bbox=[0.105, 0.243, 0.796, 0.915])

```
do {
  WriteLine("Bank balance is {0}", bankBal.ToString("C"));
  bankBal = bankBal + bankBal * INT_RATE;
  Write("Do you want to see next year's balance? Y or N...");
  inputString = ReadLine();
  response = Convert.ToChar(inputString);
} while (response == 'Y');
```

**Figure 5-13** Part of the bank balance program using a do loop

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN-022-200-212