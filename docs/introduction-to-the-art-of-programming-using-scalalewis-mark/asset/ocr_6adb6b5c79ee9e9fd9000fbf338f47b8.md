In fact, the script that we showed in the last section has the possibility for a race condition because both threads are accessing answered and timeUp with at least one writing to each. Though you could run the script many times and never see this, it is possible to answer the question, get a response, and be told that time is up in one run. To see how, picture the threads as arrows and imagine that you hit Enter at exactly the same time as the last second counts off. So the lines if(!answered) and if(!timeUp) execute at the same time. This means that both values will still be false and the program can get into both of those if statements.

Hopefully you can see how both of those examples could cause problems. However, they both require specific timing for the error to manifest. This does not make them unimportant, it just makes them hard to demonstrate. Indeed, that type of bug is one of the hardest to diagnose and fix because it is so rare and hard to reproduce. If you want to specifically see the problems that occur as a result of race conditions, the following code will do that for you.

```
var cnt = 0
val threads = Array.fill(100){
  new Thread {
    override def run {
      for(i <- 1 to 1000000) cnt += 1
    }
  }
}
threads.foreach(_.start)
threads.foreach(_.join)
println(cnt)
```

This code has a counter that starts at zero and then makes and starts 100 threads that each contain a for loop which counts to one million and as it does so it adds to the counter. At the end, the counter is printed.

Between the start and the print is a line that calls join on all the threads. The join method is designed to block until the thread it is called on finishes. After the thread finishes it continues. If this line were left out of the code, the print statement could, and likely would, happen while there were still threads adding to the counter. The use of join here simply makes sure that all the threads have finished before we do the print.

Just looking at this code it should be clear that we expect the final line to print out 100 million. However, if you run it, you will find that it never does.³ Even if you run it on a machine with only a single core, the final printout will be less than 100 million. That is because on a machine with a single core, threads can not execute at exactly the same time so instead they swap from one to the other.

# 21.2.1.2 Deadlock

The way to prevent threads from having race conditions when there is a mutable state is to lock critical parts of code so that only one thread can be in those critical sections at a given time. There are also times when you need to have some threads wait for other threads to finish before they move on to further tasks. For example, you probably should not start filling the trench with water until after all the digging is done and everyone has gotten out.

Making it so that one thread can pause and wait for another to finish doing something is critical. However, it can also lead to a situation called deadlock where different threads are

> ³Technically it could, but the odds of that happening are vanishingly small.