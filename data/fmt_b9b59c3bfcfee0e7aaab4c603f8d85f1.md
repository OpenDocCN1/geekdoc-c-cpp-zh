
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

在 Listing D.1 中，你同时使用了 `System.Threading` 和 `System.Timers` 的 using 指令。这使得 `Timer` 类型变得模糊。因此，使用别名明确将 `Timer` 与 `System.Timers.Timer` 关联。

`System.Threading.Timer` 的一个值得注意的特性是它在构造函数中接收回调委托和间隔。

## LISTING D.2: Using `System.Threading.Timer`

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

你可以通过 `Change()` 方法在 `System.Threading.Timer` 实例化后更改间隔或到期时间。然而，你不能在实例化后更改回调侦听器。相反，你必须创建新实例。

- `...` (ellipsis) binary/assignment operator, 399

- `*=` (asterisk, equal sign) binary/assignment operator, 399

- `%=` (percent sign, equal) binary/assignment operator, 399

- `/=` (slash, equal) binary/assignment operator, 399

- `&=` (ampersand, equal sign) compound assignment operator, 133-134

- `^=` (caret, equal sign) compound assignment operator, 133-134

- `|=` (vertical bar, equal sign) compound assignment operator, 133-134

- `?:` (question mark, colon) conditional operator, 123-124

- `--` (minus signs) decrement operator

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

- `/` (forward slash) division operator

  - description, 91-92

  - overloading, 397-399

  - precedence, 92

- `.` (dot) dot operator, 126, 871

- `==` (equal signs) equality operator

  - overloading, 396-397

  - in place of `=` (equal sign) assignment operator, 119-120

- `/` (forward slash) in XML, 25

- `++` (plus signs) increment operator

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

- `!=` (exclamation point, equal sign) inequality operator

  - overloading, 362, 396-397

  - testing for inequality, 119-120

- `<` (less than sign) less than operator, 120, 396-397

- `<=` (less than, equal sign) less than or equal operator, 120, 396-397

- `!` (exclamation point) logical NOT operator, 122

- `%` (percent sign) modulo, 91-92, 397-399

- `*` (asterisk) multiplication operator, 91-92, 397-399

- `?` (question mark) nullable modifier, 64-65, 459

- `??` (question marks) null-coalescing operator, 124-125, 126

- `?.` (question mark, dot) null-conditional operator, 125-128

- `|` (vertical bar) OR operator, 131, 132, 397-399

- `||` (vertical bars) OR operator, 121

- `<<=` (less than signs, equal) shift left assignment operator, 130

- `<<` (less than signs) shift left operator, 130, 397-399

- `^` (caret) XOR operator, 122, 131, 397-399

- `\` (single backslash character), escape sequence, 46

- `>` (greater than sign), greater than operator, 120, 396-397

- `>=` (greater than, equal sign), greater than or equal operator, 120, 396-397

- `=>` (equal sign, greater than) lambda operator, 517, 524

- `>>` (greater than signs), shift right operator, 130, 397-399

- `>>=` (greater than signs, equal ) shift right assignment operator, 130

- `~` (tilde) bitwise complement operator, 134

- A

- `Abort()` method, 745-746

- Aborting threads, 745-746

- Abstract classes. See also Derivation.

  - defining, 314-331

  - definition, 314

  - derived from `System.Object`, 320-321

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

- `Action` delegates, 524-525

- Activation frame, 182-183

- `Add()` method

  - appending items to lists, 648

  - inserting dictionary elements, 654-655

  - `System.Threading.Interlocked` class, 829

  - thread synchronization, 829-830

- Addresses. See Pointers and addresses.

- Aggregate functions, 618

- `AggregateException`, 557-558, 762-765

- `AggregateException.Flatten()` method, 780

- `AggregateException.Handle()` method, 764, 780

- Aggregation

  - derivation, 299-301

  - interfaces, 343-344

  - multiple inheritance, interfaces, 343-344

- Aliasing, namespaces, 179-180. See also using directive.

- `AllocExecutionBlock()` method, 857

- `AllowMultiple` member, 707

- Alternative flow control statements, 111
