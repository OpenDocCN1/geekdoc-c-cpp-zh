a List<T> of values that various tasks are calculating. One way to place the result into the correct location of the list is to store the list index targeted to contain the result into the AsyncState property. This way, when the task completes, the code can index into the list using the AsyncState (first casting it to an int). (Note that calling List<T>.Add() is not a safe operation across multiple threads, and calling it will result in a race condition that is likely to result in data loss.)

# Task.CurrentId

Task.CurrentId is a static property on the Task that returns an identifier for the currently executing Task (the one executing the Task.CurrentId call). Since the property is static, it is available anywhere and is mostly useful for debugging and diagnostic-type activities.

As discussed within the context of Task cancellation later in the chapter, additional properties on Task are also available.

# ContinueWith()

A Task includes a ContinueWith() method for chaining tasks together such that as soon as the first one in the chain completes it triggers the ones that have registered to begin executing after it. Since the ContinueWith() methods return another Task, the chain of work can continue to be added to.

It is interesting to note that it is possible to add multiple tasks using ContinueWith() and that such “continue-with” tasks are free to commence immediately upon completion of the antecedent task—the Task instance against which the ContinueWith() method was called. Furthermore, when ContinueWith() is called multiple times on the same antecedent task instance, all tasks that are added will commence running in parallel when the antecedent task completes.

The full list of available flags with descriptions from the MSDN TaskContinuationOptions documentation appears in Table 18.1. The values are flags, so they can be combined using the logical OR operator (|).

The items decorated with a star (*) are particularly useful for “registering” for “notifications” of the antecedent task’s behavior. Listing 18.3 demonstrates this.