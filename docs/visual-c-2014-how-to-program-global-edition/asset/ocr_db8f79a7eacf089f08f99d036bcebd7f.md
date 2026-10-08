# 23.3 Executing an Asynchronous Task from a GUI App

# 23.3.3 Task Method Run: Executing Asynchronously in a Separate Thread

Line 29 creates and starts a Task<TResult>(namespace System.Threading.Tasks), which returns a result of generic type TResult at some point in the future. Class is of .NET Parallel Library (TPL) for parallel and asynchronous processing. The version of Class's static method Run in method 29 creates a Func<TResult> delegate (delegates were introduced in Section 14.3.3) as an argument and executes it in a separate thread. The delegate Func<TResult> represents a method that has no arguments and returns a result of the type specified by the TResult parameter. The return type of the method you pass to Run is used by the compiler as the argument for Run's func delegate and for Task that runs

Method Fibonacci requires an argument, line 29 passes the lambda expression which takes no arguments—this encapsulates the call to Fibonacci with the argument number (the value entered by user). The lambda expression implicitly returns the Fibonacci call (a long), so it meets the Task<long> delegate's requirements. In this example, Task's static method creates and returns a Task<long>. The compiler infers the long from the return type of method Fibonacci. We declare local variable FibonacciTask(line 29) with—we explicitly used the type Task<long> for clarity, case Task method Run's return type is not obvious from the class.

# 23.3.4 awaiting the Result

Next, line 32 awaits the result of the FibonacciTask that is executing asynchronously. If the FibonacciTask is already complete, execution continues with line 35. Otherwise, control returns to clickButton_Click (the GUI event-handling thread) until the result of the FibonacciTask is available. This allows the GUI to remain responsive while the Task executes. Once the Task completes, cancelButton_Click continues at line 35, which uses property Result to get the value returned by Fibonacci and display it on asyncResultLabel.

An async method can perform statements between those that launch an asynchronous Task and await it. In such a case, the method continues executing statements after awaiting the Task until it reaches the await expression. Lines 29 and 32 are written more concisely

```
long result = await Task.Run(() => Fibonacci(number));
```

In this case, the await operator unwraps the Task's result—the long returned by method Fibonacci. You can then use the long value directly without accessing the Task's property.

# 23.3.5 Calculating the Next Fibonacci Value Synchronously

When you click Next Number, the event handler secondNumber_Click (lines 39–50) executes. Lines 42–45 add the previous two Fibonacci numbers stored in instance variables n1 and n2 to determine the next number in the sequence, update variables n1 and