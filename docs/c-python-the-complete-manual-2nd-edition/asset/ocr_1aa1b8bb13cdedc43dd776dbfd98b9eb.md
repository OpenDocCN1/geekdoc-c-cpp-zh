# # Exceptions

When coding, you'll naturally come across some issues that are out of your control. Let's assume you ask a user to divide two numbers and they try to divide by zero. This will create an error and break your code.

# ## EXCEPTIONAL OBJECTS

Rather than stop the flow of your code, Python includes exception objects which handle unexpected errors in the code. You can combat errors by creating conditions where exceptions may occur.

You can create an exception error by simply trying to divide a number by zero. This will report back with the ZeroDivisionError. Division by zero message, as seen in the screenshot. The ZeroDivisionError part is the exception class, of which there are many.

![](bbox=[0.05, 0.65, 0.45, 0.9])

Most exceptions are raised automatically when Python comes across something that's inherently wrong with the code. However, you can create your own exceptions that are designed to contain the potential error and react to it, as opposed to letting the code fail.

+   - BaseException
+   - SystemExit
+   - KeyboardInterrupt
+   - GeneratorExit
+   - StopIteration
+   - StopAsyncIteration
+   - ArithmeticError
+   - BufferError
+   - AssertionError
+   - AttributeError
+   - EOFError
+   - ImportError
+   - ModuleNotFoundError
+   - LookupError
+   - IndexError
+   - ValueError
+   - FloatingPointError
+   - OverflowError
+   - ZeroDivisionError
+   - ConnectionError
+   - BrokenPipeError
+   - ChildProcessError
+   - ConnectionAbortedError
+   - ConnectionRefusedError
+   - ConnectionResetError
+   - FileExistsError
+   - FileNotFoundError
+   - InterruptedError
+   - IsADirectoryError
+   - NotADirectoryError
+   - PermissionError
+   - ProcessLookupError
+   - TimeoutError
+   - ReferenceError
+   - RuntimeError
+   - NotImplementedError
+   - SyntaxError
+   - IndentationError
+   - TabError
+   - TypeError
+   - UnboundLocalError
+   - OSError
+   - BlockingIOError
+   - ChildProcessError
+   - ConnectionError
+   - BrokenPipeError
+   - ConnectionAbortedError
+   - ConnectionRefusedError
+   - ConnectionResetError
+   - FileExistsError
+   - FileNotFoundError
+   - InterruptedError
+   - IsADirectoryError
+   - NotADirectoryError
+   - PermissionError
+   - ProcessLookupError
+   - TimeoutError
+   - ReferenceError
+   - RuntimeError
+   - NotImplementedError
+   - SyntaxError
+   - IndentationError
+   - TabError
+   - TypeError
+   - UnboundLocalError
+   - OSError
+   - BlockingIOError

You can use the functions raise exception to create our own error handling code within Python. Let's assume your code has you warping around the cosmos, too much however results in a warp core breach. To stop the game from exiting due to the warp core going supernova, you can create a custom exception: raise Exception("warp core breach")

![](bbox=[0.5, 0.65, 0.95, 0.9])

To trap any errors in the code you can encase the potential error within a try block. This block consists of try, except, else, where the code is held within try, then if there's an exception do something, else do something else.

```
try:
    # Insert your operations here ---->
    except Exception 1:
        If there is an exception do this ---->
    except Exception 2:
        If there is another exception do this ---->
    else:
        If there is no exception, then do this ----->
```