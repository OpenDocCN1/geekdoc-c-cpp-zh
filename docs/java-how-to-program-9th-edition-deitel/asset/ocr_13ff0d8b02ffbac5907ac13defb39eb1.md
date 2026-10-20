slot. DepositSlot has no attributes and only one method—isEnvelopeReceived (lines 8–11)—which indicates whether a deposit envelope was received.

```
// DepositSlot.java
// Represents the deposit slot of the ATM

public class DepositSlot
{
    // indicates whether envelope was received (always returns true,
    // because this is only a software simulation of a real deposit slot)
    public boolean isEnvelopeReceived()
    {
        return true; // deposit envelope was received
    } // end method isEnvelopeReceived
} // end class DepositSlot
```

Fig. 13.17 | Class DepositSlot represents the ATM's deposit slot.

Recall from the requirements document that the ATM allows the user up to two minutes to insert an envelope. The current version of method isEnvelopeReceived simply returns true immediately (line 10), because this is only a software simulation, and we assume that the user has inserted an envelope within the required time frame. If an actual hardware deposit slot were connected to our system, method isEnvelopeReceived might be implemented to wait for a maximum of two minutes to receive a signal from the hardware deposit slot indicating that the user has indeed inserted a deposit envelope. If isEnvelopeReceived were to receive such a signal within two minutes, the method would return true. If two minutes elapsed and the method still had not received a signal, then the method would return false.

# 13.4.6 Class Account

Class Account (Fig. 13.18) represents a bank account. Each Account has four attributes (modeled in Fig. 13.10)—accountNumber, pin, availableBalance and totalBalance. Lines 6–9 implement these attributes as private fields. Variable availableBalance represents the amount of funds available for withdrawal. Variable totalBalance represents the amount of funds available, plus the amount of deposited funds still pending confirmation or clearance.

```
// Account.java
// Represents a bank account

public class Account
{
    private int accountNumber; // account number
    private int pin; // PIN for authentication
    private double availableBalance; // funds available for withdrawal
    private double totalBalance; // funds available + pending deposits
```

Fig. 13.18 | Class Account represents a bank account. (Part 1 of 2.)