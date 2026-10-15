

计时器到期的情况。¹ 在另外两个选项之间进行选择并不那么明显，通常两者之间的差异并不显著。如果需要在 IContainer 中托管，System.Timers.Timer 是正确的选择。然而，如果不需要特定的 System.Timers.Timer 功能，默认情况下应选择 System.Threading.Timer，因为它是一个稍轻量级的实现。

1. 理论上，使用依赖线程池的计时器也可以实现类似的延迟，因为线程池可能已经很忙。

Listing D.1 和 Listing D.2 分别提供了使用 System.Timers.Timer 和 System.Threading.Timer 的示例代码。它们的代码非常相似，包括两者都支持在 using 语句中实例化，因为两者都支持 IDisposable。两个列表的输出是相同的，出现在 Output D.1 中。其目的是显示与指示计时器触发次数的计数值的关联时间戳。完成后，输出验证计时器线程与 Main 线程不是同一个线程，以及计数的最终值。

## LISTING D.1: Using `System.Timers.Timer`

```csharp
using System;
using System.Timers;
using System.Threading;
// Because Timer exists in both the System.Timers and
// System.Threading namespaces, you disambiguate "Timer"
// using an alias directive.
using Timer = System.Timers.Timer;

class UsingSystemTimersTimer
{
    private static int _Count=0;
    private static readonly ManualResetEvent _ResetEvent =
        new ManualResetEvent(false);
    private static int _AlarmThreadId;

    public static void Main()
    {
        using (Timer timer = new Timer())
        {
            // Initialize Timer
            timer.AutoReset = true;
            timer.Interval = 1000;
            timer.Elapsed +=
                new ElapsedEventHandler(Alarm);

            timer.Start();

            // Wait for Alarm to fire for the 10th time.
            _ResetEvent.WaitOne();
        }

        // Verify that the thread executing the alarm
        // Is different from the thread executing Main
        if(_AlarmThreadId ==
            Thread.CurrentThread.ManagedThreadId)
        {
            throw new ApplicationException(
                "Thread Ids are the same.");
        }
        if(_Count < 9)
        {
            throw new ApplicationException(
                "_Count < 9");
        };

        Console.WriteLine(
            "(Alarm Thread Id) {0} != {1} (Main Thread Id)",
            _AlarmThreadId,
            Thread.CurrentThread.ManagedThreadId);
        Console.WriteLine(
            "Final Count = {0}", _Count);
    }

    static void Alarm(
        object sender, ElapsedEventArgs eventArgs)
    {
        _Count++;

        Console.WriteLine("{0}:- {1}",
            eventArgs.SignalTime.ToString("T"),
            _Count);

        if (_Count >= 9)
        {
            _AlarmThreadId =
                Thread.CurrentThread.ManagedThreadId;
            _ResetEvent.Set();
        }
    }
}
```

在 Listing D.1 中，你同时使用了 System.Threading 和 System.Timers 的 using 指令。这使得 Timer 类型变得模糊。因此，使用别名明确将 Timer 与 System.Timers.Timer 关联。

System.Threading.Timer 的一个值得注意的特性是它在构造函数中接收回调委托和间隔。

## LISTING D.2: Using System.Threading.Timer

```csharp
using System;
using System.Threading;

class UsingSystemThreadingTimer
{
    private static int _Count=0;
    private static readonly AutoResetEvent _ResetEvent =
        new AutoResetEvent(false);
    private static int _AlarmThreadId;

    public static void Main()
    {
        // Timer(callback, state, dueTime, period)
        using( Timer timer =
            new Timer(Alarm, null, 0, 1000) )
        {
            // Wait for Alarm to fire for the 10th time.
            _ResetEvent.WaitOne();
        }

        // Verify that the thread executing the alarm
        // Is different from the thread executing Main
        if(_AlarmThreadId ==
            Thread.CurrentThread.ManagedThreadId)
        {
            throw new ApplicationException(
                "Thread Ids are the same.");
        }
        if(_Count < 9)
        {
            throw new ApplicationException(
                "_Count < 9");
        };

        Console.WriteLine(
            "(Alarm Thread Id) {0} != {1} (Main Thread Id)",
            _AlarmThreadId,
            Thread.CurrentThread.ManagedThreadId);
        Console.WriteLine(
            "Final Count = {0}", _Count);
    }

    static void Alarm(object state)
    {
        _Count++;

        Console.WriteLine("{0}:- {1}",
            DateTime.Now.ToString("T"),
            _Count);

        if (_Count >= 9)
        {
            _AlarmThreadId =
                Thread.CurrentThread.ManagedThreadId;
            _ResetEvent.Set();
        }
    }
}
```

## OUTPUT D.1

```text
12:19:36 AM:- 1
12:19:37 AM:- 2
12:19:38 AM:- 3
12:19:39 AM:- 4
12:19:40 AM:- 5
12:19:41 AM:- 6
12:19:42 AM:- 7
12:19:43 AM:- 8
12:19:44 AM:- 9
(Alarm Thread Id) 4 != 1 (Main Thread Id)
Final Count = 9
```

你可以通过 Change() 方法在 System.Threading.Timer 实例化后更改间隔或到期时间。然而，你不能在实例化后更改回调侦听器。相反，你必须创建新实例。

- ... (ellipsis) binary/assignment operator, 399
- *= (asterisk, equal sign) binary/assignment operator, 399
- %= (percent sign, equal) binary/assignment operator, 399
- /= (slash, equal) binary/assignment operator, 399
- &= (ampersand, equal sign) compound assignment operator, 133-134
- ^= (caret, equal sign) compound assignment operator, 133-134
- |= (vertical bar, equal sign) compound assignment operator, 133-134
- ?: (question mark, colon) conditional operator, 123-124
- -- (minus signs) decrement operator
  - C++ vs. C#, 105
  - decrement, in a loop, 102-105
  - description, 101-102
  - guidelines, 105
  - lock statement, 105-106
  - postfix increment operator, 104-105
  - post-increment operator, 103
  - prefix increment operator, 104-105
  - pre-increment operator, 103-104
  - race conditions, 105-106
  - thread safety, 105-106
- / (forward slash) division operator
  - description, 91-92
  - overloading, 397-399
  - precedence, 92
- . (dot) dot operator, 126, 871
- == (equal signs) equality operator
  - overloading, 396-397
  - in place of = (equal sign) assignment operator, 119-120
- / (forward slash) in XML, 25
- ++ (plus signs) increment operator
  - C++ vs. C#, 105
  - decrement, in a loop, 102-105
  - description, 101-102
  - guidelines, 105
  - lock statement, 105-106
  - postfix increment operator, 104-105
  - post-increment operator, 103
  - prefix increment operator, 104-105
  - pre-increment operator, 103-104
  - race conditions, 105-106
  - thread safety, 105-106
- != (exclamation point, equal sign) inequality operator
  - overloading, 362, 396-397
  - testing for inequality, 119-120
- < (less than sign) less than operator, 120, 396-397
- <= (less than, equal sign) less than or equal operator, 120, 396-397
- ! (exclamation point) logical NOT operator, 122
- % (percent sign) modulo, 91-92, 397-399
- * (asterisk) multiplication operator, 91-92, 397-399
- ? (question mark) nullable modifier, 64-65, 459
- ?? (question marks) null-coalescing operator, 124-125, 126
- ?. (question mark, dot) null-conditional operator, 125-128
- | (vertical bar) OR operator, 131, 132, 397-399
- || (vertical bars) OR operator, 121
- <<= (less than signs, equal) shift left assignment operator, 130
- << (less than signs) shift left operator, 130, 397-399
- ^ (caret) XOR operator, 122, 131, 397-399
- \ (single backslash character), escape sequence, 46
- > (greater than sign), greater than operator, 120, 396-397
- >= (greater than, equal sign), greater than or equal operator, 120, 396-397
- => (equal sign, greater than) lambda operator, 517, 524
- >> (greater than signs), shift right operator, 130, 397-399
- >>= (greater than signs, equal ) shift right assignment operator, 130
- ~ (tilde) bitwise complement operator, 134
- A
- Abort() method, 745-746
- Aborting threads, 745-746
- Abstract classes. See also Derivation.
  - defining, 314-331
  - definition, 314
  - derived from System.Object, 320-321
  - vs. interfaces, 338
  - polymorphism, 318-320
- Abstract members
  - defining, 315-317
  - definition, 314
  - "is a" relationships, 317
  - overriding, 317
  - virtual, 317
- Access modifiers. See also Encapsulation.
  - definition, 233-235
  - on getters and setters, 251-252
  - purpose of, 236
- Action delegates, 524-525
- Activation frame, 182-183
- Add() method
  - appending items to lists, 648
  - inserting dictionary elements, 654-655
  - System.Threading.Interlocked class, 829
  - thread synchronization, 829-830
- Addresses. See Pointers and addresses.
- Aggregate functions, 618
- AggregateException, 557-558, 762-765
- AggregateException.Flatten() method, 780
- AggregateException.Handle() method, 764, 780
- Aggregation
  - derivation, 299-301
  - interfaces, 343-344
  - multiple inheritance, interfaces, 343-344
- Aliasing, namespaces, 179-180. See also using directive.
- AllocExecutionBlock() method, 857
- AllowMultiple member, 707
- Alternative flow control statements, 111
- Ampersand, equal sign (&=) compound assignment operator, 133-134
- Ampersand (&) AND operator, 131, 132
- Ampersands (&&) AND operator, 121
- Angle brackets (< >), in XML, 25
- Anonymous functions
  - definition, 516, 517
  - guidelines, 533
- Anonymous methods. See also Lambda expressions.
  - definition, 522
  - guidelines, 523
  - internals, 527-528
  - parameterless, 523
  - passing, 522-523
- Anonymous types
  - definition, 61, 572
  - explicit local variables, 263-265
  - generating, 578
  - implicit local variables, 572-576
  - in query expressions, 625-626
  - type incompatibilities, 576-577
  - type safety, 576-577
  - var keyword, 572-576
- Antecedent tasks, 757
- Apartment-threading models, 846
- APIs (application programming interfaces)
  - calls from P/Invoke, wrappers, 860-861
  - definition, 25
  - deprecated, 712
  - as frameworks, 26
- Append method, 58
- AppendFormat method, 58
- Appending items to collections, 648
- Applicable method calls, 201
- Applications, compiling, 3
- Appointment, 291-292
- __ arglist keyword, 8
- ArgumentNullException, 434-435, 436
- ArgumentOutOfRangeException, 435, 436
- Arguments
  - calling methods, 163, 167-168
  - named, calling methods, 199
- Arity (number of type parameters), 471-472
- Array accessor, 78-79
- Array declaration
  - C++ vs. C#, 72-74
  - code example, 78-79
  - Java vs. C#, 72-74
- Array types, constraint limitations, 484
- ArrayList type, 363-365
- Arrays. See also Collections; Lists; TicTacToe game.
  - accessing elements of, 73, 78-79
  - of arrays, 78
  - assigning values to, 73-76
  - binary search, 81-83
  - BinarySearch() method, 81-83
  - Clear() method, 81-83
  - clearing, 81-83
  - common errors, 86-87
  - converting collections to, 646
  - description, 71-72

