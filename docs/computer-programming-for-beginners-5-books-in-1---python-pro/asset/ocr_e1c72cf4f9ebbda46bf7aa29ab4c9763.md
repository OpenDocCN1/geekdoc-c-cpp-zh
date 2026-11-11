When all transactions are completed, any changes or modifications must be preserved and maintained. In the event of hardware or application error, there should be no loss of data; it should be available reliably and consistently. This characteristic ensures that your data is available in the event of such

One has to note that at any time, whether operations are completed or reverted, the transaction maintains the integrity of the database.

There are seven commands that you can use to manage transactions. These are:

**COMMIT:** Saves changes and commits them to the database.

**ROLLBACK:** Rolls back changes to a specific SAVEPOINT, or the beginning of a transaction. Changes are not applied to the database.

**SAVEPOINT:** Creates a savepoint – a form of marker – within a transaction. When you ROLLBACK, you can reach this point instead of the beginning of the transaction.

**RELEASE SAVEPOINT:** Removes or releases a savepoint. After this command, any ROLLBACK will revert the transaction to its original state.

**SET TRANSACTION:** Creates characteristics for the execution of a particular transaction.

**START TRANSACTION:** Sets the characteristics of the transactions and begins the transaction.

**SET CONSTRAINTS:** Establishes the constraint mode within a transaction. A constraint creates a condition where a decision is passed to either apply the constraint as soon as modifications on the data begin to occur or delay the application of the constraint until the completion of the transaction.

Time for another example.

It is important to remember that when you are about to start a transaction, the database is in its original state. At this state, you can expect the data to be consistent. Once you execute the transactions, the SQL statements within those transactions begin processing. If the process is successful, then one uses the COMMIT command. This command causes the SQL statements to update the database and dismiss the transaction. If the process of updating is not successful, then the ROLLBACK command comes into play. This process gives you a brief overview of commands. However, we will be going in-depth into their functions.

# Commit