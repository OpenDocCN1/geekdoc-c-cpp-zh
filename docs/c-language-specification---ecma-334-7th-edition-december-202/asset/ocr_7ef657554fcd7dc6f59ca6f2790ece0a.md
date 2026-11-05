> Note: An await_expression cannot occur in most places within a query_expression, because those are syntactically transformed to use non-async lambda expressions. end note

Inside an async function, await shall not be used as an available_identifier although the verbatim identifier @await may be used. There is therefore no syntactic ambiguity between await_expressions and various expressions involving identifiers. Outside of async functions, await acts as a normal identifier.

The operand of an await_expression is called the task. It represents an asynchronous operation that may or may not be complete at the time the await_expression is evaluated. The purpose of the await operator is to suspend execution of the enclosing async function until the awaited task is complete, and then obtain its outcome.

# 12.9.8.2 Awaitable expressions

The task of an await_expression is required to be awaitable. An expression t is awaitable if one of the following holds:

+   - t is of compile-time type dynamic
+   - t has an accessible instance or extension method called GetAwaiter with no parameters and no type parameters, and a return type A for which all of the following hold:
+     - A implements the interface System.Runtime.CompilerServices.INotifyCompletion (hereafter known as INotifyCompletion for brevity)
+     - A has an accessible, readable instance property IsCompleted of type bool
+     - A has an accessible instance method GetResult with no parameters and no type parameters

The purpose of the GetAwaiter method is to obtain an awaiter for the task. The type A is called the awaiter type for the await expression.

The purpose of the IsCompleted property is to determine if the task is already complete. If so, there is no need to suspend evaluation.

The purpose of the INotifyCompletion.OnCompleted method is to sign up a "continuation" to the task; i.e., a delegate (of type System.Action) that will be invoked once the task is complete.

The purpose of the GetResult method is to obtain the outcome of the task once it is complete. This outcome may be successful completion, possibly with a result value, or it may be an exception which is thrown by the GetResult method.

# 12.9.8.3 Classification of await expressions

# 12.9.8.4 Run-time evaluation of await expressions

At run-time, the expression await t is evaluated as follows:

+   - An awaiter a is obtained by evaluating the expression (t).GetAwaiter().
+   - A bool b is obtained by evaluating the expression (a).IsCompleted.
+   - If b is false then evaluation depends on whether a implements the interface System.Runtime.CompilerServices.ICriticalNotifyCompletion (hereafter known as ICriticalNotifyCompletion for brevity). This check is done at binding time; i.e., at run-time if a has