7. **Name the new class and then click the Finish button.**

For example, you can name your class filename Account.m, as shown in Figure 7-4.

8. **Open the BankAccount.h file and add this code:**

```
```objective-c
#import <Cocoa/Cocoa.h>

@interface Account : NSObject {
    float balance;
}

-(float) balance;
-(void) setBalance: (float) aBalance;

-(void) deposit: (float) anAmount;
-(void) withdraw: (float) withdrawAmount;

@end
```
```

This code defines a balance as an instance variable, adds accessor methods for the balance so the Controller object can retrieve and set the balance, and includes a couple methods for depositing and withdrawing money from the account.

![](bbox=[0.25, 0.53, 0.74, 0.85])

# Figure 7-4:
Name the
new class
filename
Account.m.