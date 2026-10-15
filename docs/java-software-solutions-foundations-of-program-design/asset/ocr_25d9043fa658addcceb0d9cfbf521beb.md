transactions on the account, adjusting the balance based on the parameters. There is also an addInterest method that updates the balance by adding in the interest earned. These methods represent valid ways to change the balance, so a classic mutator such as setBalance is not provided.

The status of the three Account objects just after they were created in the Transactions program could be depicted as follows:

![](bbox=[0.05, 0.35, 0.95, 0.7])

The various methods that update the balance of the account could be more rigorously designed. Checks should be made to ensure that the parameter values are valid, such as preventing the withdrawal of a negative amount (which would essentially be a deposit). This processing is discussed in the next chapter.

+   SR 4.16 Why a method invoked through (or on) a particular object? What is the exception to that rule?
+   
+   SR 4.17 What does it mean for a method to return a value?
+   
+   SR 4.18 What does the return statement do?
+   
+   SR 4.19 Is a return statement required?