The default isolation level that is applied to the transaction is ReadCommitted. The following table shows the different options you can set.

| Isolation Level | Description |
|---|---|
| ReadUncommitted | Transactions are not isolated from each other. With this level, there is no wait for locked records from other transactions. This way, uncommitted data can be read from other transactions—dirty reads. This level is usually only used for reading records for which it does not matter if you read interim changes, such as reports. |
| ReadCommitted | Waits for records with a write-lock from other transactions. This way, a dirty read cannot happen. This level sets a read-lock for the current record read and a write-lock for the records being written until the transaction is completed. During the reading of a sequence of records, with every new record that is read, the prior record is unlocked. That’s why nonrepeatable reads can happen. |
| RepeatableRead | Holds the lock for the records read until the transaction is completed. This way, the problem of nonrepeatable reads is avoided. Phantom reads can still occur. |
| Serializable | Holds a range lock. While the transaction is running, it is not possible to add a new record that belongs to the same range from which the data is being read. |
| Snapshot | With this level a snapshot is done from the actual data. This level reduces the locks as modified rows are copied. That way, other transactions can still read the old data without needing to wait for releasing of the lock. |
| Unspecified | Indicates that the provider is using an isolation level that is different from the values defined by the IsolationLevel enumeration. |
| Chaos | This level is similar to ReadUncommitted, but in addition to performing the actions of the ReadUncommitted value, Chaos does not lock updated records. |

The following table summarizes the problems that can occur as a result of setting the most commonly used transaction isolation levels.