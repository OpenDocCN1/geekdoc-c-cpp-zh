```
```cpp
34    std::cout << '\\n';

35
36    std::thread t1(setDataReady);
37    std::thread t2(waitingForWork);

38
39    t1.join();
40    t2.join();

41
42    std::cout << '\\n';

43
44 }
```
```

By chance, the first invocation of the program works fine. The second invocation locks because the notify call (line 28) happens before the thread t2 (line 37) is waiting (line 19).

![](bbox=[0.303, 0.389, 0.697, 0.566])

A blocking condition variable

Of course, deadlocks and livelocks are side effects of race conditions. A deadlock depends in general on the interleaving of the threads and may sometimes occur or not. A livelock is similar to a deadlock. While a deadlock blocks, a livelock seems to make progress, emphasizing “seems”. Think about a transaction in a transactional memory use case. Each time the transaction should be committed, a conflict happens; therefore, a rollback takes place. Here are the details of transactions.

# 15.3 Breaking of Program Invariants

Program invariants are invariants that should hold for the entire lifetime of your program.

Malicious race condition breaks an invariant of the program. The invariant of the program is that the sum of all balances should be the same amount. Which in our case is 200 euros because each account starts with 100 euro (line 9). I neither want to create money by transferring it, nor do I want to destroy it.