Here are the general forms for Pulse() and PulseAll():

```
public static void Pulse(object waitOb)
public static void PulseAll(object waitOb)
```

Here, waitOb is the object being released.

A SynchronizationLockException will be thrown if Wait(), Pulse(), or PulseAll() is called from code that is not within synchronized code, such as a lock block.

# An Example That Uses Wait() and Pulse()

To understand the need for and the application of Wait() and Pulse(), we will create a program that simulates the ticking of a clock by displaying the words "Tick" and "Tock" on the screen. To accomplish this, we will create a class called TickTock that contains two methods: Tick() and Tock(). The Tick() method displays the word "Tick" and Tock() displays "Tock". To run the clock, two threads are created, one that calls Tick() and one that calls Tock(). The goal is to make the two threads execute in a way that the output from the program displays a consistent "Tick Tock"—that is, a repeated pattern of one "Tick" followed by one "Tock."

```
// Use Wait() and Pulse() to create a ticking clock.
using System;
using System.Threading;

class TickTock {
    object lockOn = new object();

    public void Tick(bool running) {
        lock(lockOn) {
            if(!running) { // stop the clock
                Monitor.Pulse(lockOn); // notify any waiting threads
                return;
            }

            Console.Write("Tick ");
            Monitor.Pulse(lockOn); // let Tock() run
            Monitor.Wait(lockOn); // wait for Tock() to complete
        }
    }
    public void Tock(bool running) {
        lock(lockOn) {
            if(!running) { // stop the clock
                Monitor.Pulse(lockOn); // notify any waiting threads
                return;
            }

            Console.WriteLine("Tock");
            Monitor.Pulse(lockOn); // let Tick() run
            Monitor.Wait(lockOn); // wait for Tick() to complete
        }
    }
}
```