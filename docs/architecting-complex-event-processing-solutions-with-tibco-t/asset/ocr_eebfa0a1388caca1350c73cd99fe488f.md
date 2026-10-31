![](bbox=[0.2, 0.15, 0.88, 0.55])

Figure 7-7: Query Agent Continuous Query Configuration

TinyTransaction events are of interest, new events should be added, and they should be retained in the buffer for one hour. The where clause is reevaluated whenever the buffer contents change.

# Listing 7-4: Continuous Query Example

```
select
  giantTransaction.accountNumber
from
  /Events/GiantTransaction {
    policy: maintain last 1 hours;
    accept:new) giantTransaction,
  /Events/TinyTransaction {
    policy:maintain last 1 hours;
    accept:new) tinyTransaction
  }
where
  giantTransaction.accountNumber = tinyTransaction.accountNumber and
  giantTransaction.transactionDateTime >
  tinyTransaction.transactionDateTime";
```

# Buffer Management

The logic for determining the buffer content is defined in the from clause of the query. There are two management strategies: explicit and implicit.