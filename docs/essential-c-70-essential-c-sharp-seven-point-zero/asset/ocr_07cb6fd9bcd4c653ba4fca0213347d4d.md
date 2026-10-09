Use conditional clauses with caution; if the conditional expression itself throws an exception, then that new exception is ignored and the condition is treated as false. For this reason, you should avoid throwing exceptions for the exception conditional expression.

Catch blocks must appear in order, from most specific to most general, to avoid a compile-time error. For example, moving the catch(Exception...) block before any of the other exceptions will result in a compile error, since all prior exceptions derive from System.Exception at some point in their inheritance chain.

As shown with the catch (SystemException){ } block, a named parameter for the catch block is not required. In fact, a final catch without even the type parameter is allowable, as you will see in the next section.

# ## Rethrowing an Existing Exception

In the InvalidOperationException catch block, a throw statement appears without any identification of the exception to throw (throw is on its own), even though an exception instance (exception) appears in the catch block scope that could be rethrown. Throwing a specific exception would update all the stack information to match the new throw location. As a result, all the stack information indicating the call site where the exception originally occurred would be lost, making it significantly more difficult to diagnose the problem. For this reason, C# supports a throw statement or expression (C# 7.0 or later) without the explicit exception reference as long as it occurs within a catch block. This way, code can examine the exception to determine if it is possible to fully handle it, and if not, rethrow the exception (even though not specified explicitly) as though it was never caught and without replacing any stack information.

# ADVANCED TOPIC

# ### Throwing Existing Exceptions without Replacing Stack Information

In C# 5.0, a mechanism was added that enables the throwing of a previ-ously thrown exception without losing the stack trace information in the original exception. This allows you to rethrow exceptions, for example,