action, because the association with the Keypad applies only to classes Withdrawal and Deposit, and the association with the CashDispenser applies only to class Withdrawal.

Our class diagram incorporating inheritance (Fig. 13.28) also models Deposit and BalanceInquiry. We show associations between Deposit and both the DepositSlot and the Keypad. Note that class BalanceInquiry takes part in no associations other than those inherited from class Transaction—a BalanceInquiry interacts only with the BankDatabase and the Screen.

The class diagram of Fig. 9.20 showed attributes and operations with visibility markers. Now we present a modified class diagram in Fig. 13.29 that includes abstract base class Transaction. This abbreviated diagram does not show inheritance relationships (these appear in Fig. 13.28), but instead shows the attributes and operations after we have employed inheritance in our system. Note that abstract class name Transaction and abstract operation name execute in class Transaction appear in italics. To save space, as

![](bbox=[0.168, 0.357, 0.838, 0.915])

**Fig. 13.29**  |  Class diagram after incorporating inheritance into the system.