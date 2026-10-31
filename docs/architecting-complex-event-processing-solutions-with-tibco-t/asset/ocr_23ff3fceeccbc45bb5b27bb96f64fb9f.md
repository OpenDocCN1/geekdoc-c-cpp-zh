```
Events.GiantTransaction.
    GiantTransaction(
        null,
        null,
        transaction.accountNumber,
        transaction.transactionAmount,
        transaction.transactionDateTime);
    System.debugOut("Created giant transaction: " + giantTransaction@id);
    Event.assertEvent(giantTransaction);
    System.debugOut("Asserted giant transaction: " + giantTransaction@id);
}
System.debugOut("About to consume transaction: " + transaction@id);
Event.consumeEvent(transaction);
System.debugOut("Consumed transaction: " + transaction@id);
}
```

This preprocessor function is doing two things: It is both classifying and filtering transactions. By classifying the transactions, it is making clear to the rule which transactions are below the lower threshold and which ones are above the large threshold. It is also filtering transactions: Any transaction between the two thresholds is simply consumed.

Asserting the tiny and giant transactions (which are configured with a time-to-live of one hour) triggers a new version of the Fraud Rule (Listing 5-5). This rule simply compares the account numbers and determines the order in which the transactions occurred. The determination as to whether each transaction was below the lower threshold or above the upper threshold was done in the preprocessor. Furthermore, the events will exist for only an hour, and thus the age of the transactions does not need to be determined.

# Listing 5-5: ACEPSTLocalChannel Fraud Rule

```
rule Rules.Fraud {
    attribute {
        priority = 5;
        forwardChain = true;
    }
    declare {
        Events.GiantTransaction giantTransaction;
        Events.TinyTransaction tinyTransaction;
    }
    when {
        tinyTransaction.accountNumber ==
            giantTransaction.accountNumber;
        giantTransaction.transactionDateTime >
```