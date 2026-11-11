```
```java
Math.random());
}
}
catch (InterruptedException e)
{
}
};
var t = new Thread(r);
t.start();
}
}
}
```
```

# 12.4.2 The Race Condition Explained

In the previous section, we ran a program in which several threads updated bank account balances. After a while, errors crept in and some amount of money was either lost or spontaneously created. This problem occurs when two threads are simultaneously trying to update an account. Suppose two threads simultaneously carry out the instruction

```
```java
accounts[to] += amount;
```
```

The problem is that these are not *atomic* operations. The instruction might be processed as follows:

+   1. Load `accounts[to]` into a register.
+   2. Add `amount`.
+   3. Move the result back to `accounts[to]`.

Now, suppose the first thread executes Steps 1 and 2, and then it is preempted. Suppose the second thread awakens and updates the same entry in the account array. Then, the first thread awakens and completes its Step 3.

That action wipes out the modification of the other thread. As a result, the total is no longer correct (see *Figure 12.2*).