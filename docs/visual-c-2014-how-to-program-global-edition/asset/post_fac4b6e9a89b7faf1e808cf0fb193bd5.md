
# Self-Review Exercises

- available entity
- block a calling method
- callback method
- CancelPendingRequests method of class HttpClient
- concurrency
- concurrent operations
- Descendants method of class XDocument
- exponential complexity
- Fibonacci series
- Func<TResult> delegate
- GetByteArrayAsync method of class HttpClient
- GetStringAsync method of class HttpClient
- Invoke method of class Control
- InvokeRequired method of class Control
- MethodInvoke delegate
- Maximum property of class ProgressBar
- Minimum property of class ProgressBar
- multithreading
- parallel operations
- Parse method of class XDocument
- performing operations concurrently
- ProgressBar class
- responsive GUI
- REST web service
- Result property of class Task
- Run method of class Task
- System.Net.Http namespace
- System.Threading namespace
- Task class
- Task Parallel Library
- thread of execution
- Value property of class XAttribute
- Value property of class ProgressBar
- web service
- WhenAll1 method of class Task
- WhenAny method of class Task
- XAttribute class
- XDocument class
- XElement class

# Self-Review Exercises

- **23.1** What does it mean to process tasks asynchronously?
- **23.2** What is the key advantage of programming your apps for multicore systems?
- **23.3** Suppose you program an app with two compute-intensive tasks that run on one core of a dual-core system. Then, you program the app so that the two compute-intensive tasks run asynchronously in separate threads on a dual-core system. You should expect the latter to run in half the time? Why?
- **23.4** Does the async and await mechanism create new threads?
- **23.5** (True/False) You can update a GUI from any thread of execution. If *false*, explain why.

# Answers to Self-Review Exercises

- **23.1** It means that the tasks can proceed independently of one another.
- **23.2** In multicore systems, the hardware can put multiple cores to work simultaneously, thereby enabling faster completion of tasks that can be implemented with asynchronous tasks.
- **23.3** There's no overhead inherent in using threads to perform separate tasks. Simply performing the asynchronous on a dual-core system does not complete the task in half the time, though they'll run faster than if you perform the tasks in sequence.
- **23.4** No. The method that you call to start an asynchronous task is one you *await* the result for creating new tasks.
- **23.5** False. When updating a control from a non-GUI thread, you must schedule that update to be performed by the GUI thread. To do so, you check the Form's inherited *Invoke* property. If this property's value is true, the code is executing in a non-GUI thread and must not update the GUI directly. Instead, you call Form's inherited *Invoke* method, which receives as an argument a *Delegate* representing a method to invoke.

# 1014 Chapter 23 Asynchronous Programming with async and await

# Exercises

23.6 Investigate other compute-intensive calculations, then modify the example of Fig. 23.1 to perform a different compute-intensive calculation asynchronously.

23.7 Modify the example of Fig. 23.3 to process the results using the array returned by the Task produced by Task method when awaitAll.

23.8 Investigate other web services at a site like http://www.programmableweb.com. Locate a REST service that returns XML, then modify the example of Fig. 23.4 to invoke the web service asynchronously using the methods of class `HttpClient`. Parse the results using LINQ to XML, then display the results as as appropriate for the type of data returned.

23.9 You have noticed that the prime-number example in Fig. 23.6 produces prime numbers rapidly. although that is, the speed of displaying the results on the screen slows down the program, not the ability of the computer to determine the prime number. Reimplement the example of Fig. 23.6 with a compute bound algorithm such as the recursive Fibonacci calculation of Fig. 23.1. When you run the app, the Fibonacci numbers get higher; the calculation slows dramatically, slowing the updates of the ProgressBar and the TextBox that shows the calculation results. This calculation is bound, the overall speed of the app on your processor—you want to decrease or increase the large Fibonacci number the app calculation accordingly. For example, on our computer the Fibonacci of 47 takes minutes to calculate.

23.10 Visit https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes to learn more about the Sieve of Eratosthenes. The algorithm as implemented in Fig. 23.6 is inefficient, because it keeps eliminating multiples of primes even after the array already represents all primes up to the maximum value less than or equal to the square root of the maximum value. Make the following modifications to Fig. 23.6:

- a) Update the algorithm to eliminate multiples of primes that are less than or equal to the square root of the maximum value.
- b) Modify the code that updates the ProgressBar and percentage Label so that they they indicate the progress of the Sieve of Eratosthenes algorithm, rather than the progress of checking each number in the range is prime.

![](img/57baed2319be0bb1b5f98674846f2711_1015_0.png)

# Chapters on the Web

Additional chapters are available as PDF documents¹ on this book’s Companion Website:
http://www.pearsonglobaleditions.com/deitel

Once at this site, select Visual C# How to Program, 6/e to view links to the book’s Companion Website and code examples.

New copies of this book come with a Companion Website access code that is located on the book’s inside front cover. If the access code is already visible or there is no card, you purchased a used book or an edition that does not come with an access code.

1. These files can be viewed in Adobe Reader® (http://get.adobe.com/reader).

# Operator Precedence Chart

Operators are shown in decreasing order of precedence from top to bottom with each level of precedence separated by a horizontal line. The associativity of the operators is shown in the right column.

| Operator | Type | Associativity |
| --- | --- | --- |
| . | member access | left-to-right |
| ? | null-conditional member access | |
| O | method call | |
| [] | element access | |
| ?[] | null-conditional element access | |
| ++ | postfix increment | |
| -- | postfix decrement | |
| nameof | string representation of an identifier | |
| new | object creation | |
| typeof | get System.Type object | |
| typeof |
| checked | checked evaluation | |
| unchecked | unchecked evaluation | |
| + | unary plus | left-to-right |
| - | unary minus | |
| ! | logical negation | |
| ~ | bitwise complement | |
| ++ | prefix increment | |
| -- | postfix decrement | |
| (type) | cast | |
| * | multiplication | left-to-right |
| / | division | |
| % | remainder | |

> **Fig. A.1** | Operator precedence (Part 1 of 2).

# Operator Precedence Chart

| Operator | Type | Associativity |
|---|---|---|
| + | addition | left-to-right |
| - | subtraction | |
| >> | right shift | left-to-right |
| << | left shift | left-to-right |
| < | less than | left-to-right |
| > | greater than | |
| <= | less than or equal to | |
| >= | greater than or equal to | |
| != | type comparison | |
| as | type conversion | |
| != | is not equal to | left-to-right |
| == | is equal to | |
| & | logical AND | left-to-right |
| ^ | logical XOR | left-to-right |
| \| | logical OR | left-to-right |
| && | conditional AND | left-to-right |
| || | conditional OR | left-to-right |
| ?? | null coalescing | right-to-left |
| ?: | conditional | right-to-left |
| = | assignment | right-to-left |
| *= | multiplication assignment | |
| /= | division assignment | |
| %= | remainder assignment | |
| += | addition assignment | |
| -= | subtraction assignment | |
| <<= | left shift assignment | |
| >== | right shift assignment | |
| &= | logical AND assignment | |
| ^= | logical XOR assignment | |
| |= | logical OR assignment | |

> **Fig. A.1** | Operator precedence chart (Part 2 of 2).
[/content]
```
Wait, I noticed a small error in my manual assembly of the first table. Let me provide the final cleaned version without the duplicate table fragment.

```content
[content]
# Self-Review Exercises

- available entity
- block a calling method
- callback method
- CancelPendingRequests method of class HttpClient
- concurrency
- concurrent operations
- Descendants method of class XDocument
- exponential complexity
- Fibonacci series
- Func<TResult> delegate
- GetByteArrayAsync method of class HttpClient
- GetStringAsync method of class HttpClient
- Invoke method of class Control
- InvokeRequired method of class Control
- MethodInvoke delegate
- Maximum property of class ProgressBar
- Minimum property of class ProgressBar
- multithreading
- parallel operations
- Parse method of class XDocument
- performing operations concurrently
- ProgressBar class
- responsive GUI
- REST web service
- Result property of class Task
- Run method of class Task
- System.Net.Http namespace
- System.Threading namespace
- Task class
- Task Parallel Library
- thread of execution
- Value property of class XAttribute
- Value property of class ProgressBar
- web service
- WhenAll1 method of class Task
- WhenAny method of class Task
- XAttribute class
- XDocument class
- XElement class

# Self-Review Exercises

- **23.1** What does it mean to process tasks asynchronously?
- **23.2** What is the key advantage of programming your apps for multicore systems?
- **23.3** Suppose you program an app with two compute-intensive tasks that run on one core of a dual-core system. Then, you program the app so that the two compute-intensive tasks run asynchronously in separate threads on a dual-core system. You should expect the latter to run in half the time? Why?
- **23.4** Does the async and await mechanism create new threads?
- **23.5** (True/False) You can update a GUI from any thread of execution. If *false*, explain why.

# Answers to Self-Review Exercises

- **23.1** It means that the tasks can proceed independently of one another.
- **23.2** In multicore systems, the hardware can put multiple cores to work simultaneously, thereby enabling faster completion of tasks that can be implemented with asynchronous tasks.
- **23.3** There's no overhead inherent in using threads to perform separate tasks. Simply performing the asynchronous on a dual-core system does not complete the task in half the time, though they'll run faster than if you perform the tasks in sequence.
- **23.4** No. The method that you call to start an asynchronous task is one you *await* the result for creating new tasks.
- **23.5** False. When updating a control from a non-GUI thread, you must schedule that update to be performed by the GUI thread. To do so, you check the Form's inherited *Invoke* property. If this property's value is true, the code is executing in a non-GUI thread and must not update the GUI directly. Instead, you call Form's inherited *Invoke* method, which receives as an argument a *Delegate* representing a method to invoke.

# 1014 Chapter 23 Asynchronous Programming with async and await

# Exercises

23.6 Investigate other compute-intensive calculations, then modify the example of Fig. 23.1 to perform a different compute-intensive calculation asynchronously.

23.7 Modify the example of Fig. 23.3 to process the results using the array returned by the Task produced by Task method when awaitAll.

23.8 Investigate other web services at a site like http://www.programmableweb.com. Locate a REST service that returns XML, then modify the example of Fig. 23.4 to invoke the web service asynchronously using the methods of class `HttpClient`. Parse the results using LINQ to XML, then display the results as as appropriate for the type of data returned.

23.9 You have noticed that the prime-number example in Fig. 23.6 produces prime numbers rapidly. although that is, the speed of displaying the results on the screen slows down the program, not the ability of the computer to determine the prime number. Reimplement the example of Fig. 23.6 with a compute bound algorithm such as the recursive Fibonacci calculation of Fig. 23.1. When you run the app, the Fibonacci numbers get higher; the calculation slows dramatically, slowing the updates of the ProgressBar and the TextBox that shows the calculation results. This calculation is bound, the overall speed of the app on your processor—you want to decrease or increase the large Fibonacci number the app calculation accordingly. For example, on our computer the Fibonacci of 47 takes minutes to calculate.

23.10 Visit https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes to learn more about the Sieve of Eratosthenes. The algorithm as implemented in Fig. 23.6 is inefficient, because it keeps eliminating multiples of primes even after the array already represents all primes up to the maximum value less than or equal to the square root of the maximum value. Make the following modifications to Fig. 23.6:

- a) Update the algorithm to eliminate multiples of primes that are less than or equal to the square root of the maximum value.
- b) Modify the code that updates the ProgressBar and percentage Label so that they they indicate the progress of the Sieve of Eratosthenes algorithm, rather than the progress of checking each number in the range is prime.

![](img/57baed2319be0bb1b5f98674846f2711_1015_0.png)

# Chapters on the Web

Additional chapters are available as PDF documents¹ on this book’s Companion Website:
http://www.pearsonglobaleditions.com/deitel

Once at this site, select Visual C# How to Program, 6/e to view links to the book’s Companion Website and code examples.

New copies of this book come with a Companion Website access code that is located on the book’s inside front cover. If the access code is already visible or there is no card, you purchased a used book or an edition that does not come with an access code.

1. These files can be viewed in Adobe Reader® (http://get.adobe.com/reader).

# Operator Precedence Chart

Operators are shown in decreasing order of precedence from top to bottom with each level of precedence separated by a horizontal line. The associativity of the operators is shown in the right column.

| Operator | Type | Associativity |
| --- | --- | --- |
| . | member access | left-to-right |
| ? | null-conditional member access | |
| O | method call | |
| [] | element access | |
| ?[] | null-conditional element access | |
| ++ | postfix increment | |
| -- | postfix decrement | |
| nameof | string representation of an identifier | |
| new | object creation | |
| typeof | get System.Type object | |
| sizeof | get size in bytes of a type | |
| checked | checked evaluation | |
| unchecked | unchecked evaluation | |
| + | unary plus | left-to-right |
| - | unary minus | |
| ! | logical negation | |
| ~ | bitwise complement | |
| ++ | prefix increment | |
| -- | postfix decrement | |
| (type) | cast | |
| * | multiplication | left-to-right |
| / | division | |
| % | remainder | |

> **Fig. A.1** | Operator (Part 1 of 2).

# Operator Precedence Chart

| Operator | Type | Associativity |
|---|---|---|
| + | addition | left-to-right |
| - | subtraction | |
| >> | right shift | left-to-right |
| << | left shift | left-to-right |
| < | less than | left-to-right |
| > | greater than | |
| <= | less than or equal to | |
| >= | greater than or equal to | |
| != | type comparison | |
| as | type conversion | |
| != | is not equal to | left-to-right |
| == | is equal to | |
| & | logical AND | left-to-right |
| ^ | logical XOR | left-to-right |
| \| | logical OR | left-to-right |
| && | conditional AND | left-to-right |
| || | conditional OR | left-to-right |
| ?? | null coalescing | right-to-left |
| ?: | conditional | right-to-left |
| = | assignment | right-to-left |
| *= | multiplication assignment | |
| /= | division assignment | |
| %= | remainder assignment | |
| += | addition assignment | |
| -= | subtraction assignment | |
| <<= | left shift assignment | |
| >== | right shift assignment | |
| &= | logical AND assignment | |
| ^= | logical XOR assignment | |
| |= | logical OR assignment | |

> **Fig. A.1** | Operator precedence chart (Part 2 of 2).
