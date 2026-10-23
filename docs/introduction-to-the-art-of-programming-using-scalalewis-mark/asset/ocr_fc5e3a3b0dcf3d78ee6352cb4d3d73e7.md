is being called on though as that will be the object the monitor is locked on and using the wrong one can lead to incorrect results.
As a first example, let us look at how we would fix the bank account class to be syn-
chronized so that we do not have to worry about deposits and withdrawals happening at the same time.

```
```scala
/**
 * A class that represents a bank account. The balance is stored as an Int
 * representing a number of cents.
 */
class BankAccount(private var bal:Int = 0) {
  def balance:Int = bal
  def deposit(amount:Int) = synchronized {
    assert(amount>=0)
    val oldBalance = balance
    val newBalance = oldBalance+amount
    bal = newBalance
  }
  def withdraw(amount:Int) = synchronized {
    assert(amount>=0 && amount<=bal)
    val oldBalance = balance
    val newBalance = oldBalance-amount
    bal = newBalance
  }
}
```
```

As you see, all we did here was put a call to synchronize around the full method for deposit and withdraw. An equal sign was added because we are no longer using the short syntax for a method that returns Unit. That is all that is required for that example.
You might wonder why it is that synchronization works when the code we wrote before that used an if to check a variable then automatically set it does not. The reason behind this is that the checking and setting of the lock on the monitor is an atomic operation. What does it mean for an operation to be atomic? The Greek root of the word atom means indivisible. The name was given to the particles because it was believed at the time that they were the smallest pieces of matter and could not be split. While that turns out to not really be true of atoms in nature, it is true of atomic operations on a computer. In this alternate sense, when we say it can not be split, we mean it can not be interrupted. Once an atomic operation begins, nothing else can take over before it finishes. The problem with the if followed by a set was that it was not atomic and it was possible for the value of the variable to be changed by another thread between when this thread read the value, looked at it, and set it.
So what about the example that adds to a counter in multiple threads? Given what we have seen, your first attempt might look like this.

```
```scala
var cnt = 0
val threads = Array.fill(100){
  new Thread {
    override def run {
      for(i <- 1 to 1000000) synchronized {cnt += 1}
    }
  }
}
```
```