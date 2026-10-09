Unfortunately, this asynchrony comes at the cost of complexity. Interspersed throughout the code is TPL-related code that interrupts the flow. Rather than simply following the WebRequest.GetResponseAsync() call with steps to retrieve the StreamReader and call ReadToEndAsync(), the asynchronous version of the code requires ContinueWith() statements. The first ContinueWith() statement identifies what to execute after the WebRequest.GetResponseAsync(). Notice that the reeturn statement in the first ContinueWith() expression returns StreamReader.ReadToEndAsync(), which returns another Task.

Without the Unwrap() call, therefore, the antecedent in the second ContinueWith() statement is a Task<Task<string>>, which alone indicates the complexity. As a result, it is necessary to call Result twice—once on the antecedent directly and a second time on the Task<string>.Result property antecedent.Result returned, with the latter blocking subsequent execution until the ReadToEnd() operation completes. To avoid the Task<Task<Result>> structure, we preface the call to ContinueWith() with a call to Unwrap(), thereby shedding the outer Task and appropriately handling any error or cancellation requests.

The complexity doesn't stop with Tasks and ContinueWith(), however: The exception handling adds an entirely new dimension to the complexity. As mentioned earlier, the TPL generally throws an AggregateException exception because of the possibility that an asynchronous operation could encounter multiple exceptions. However, because we are calling the Result property from within ContinueWith() blocks, it is possible that inside the worker thread we might also throw an AggregateException.

As you learned earlier in the chapter, there are multiple ways to handle these exceptions:

+   1. We can add continuation tasks to all *Async methods that return a task along with each ContinueWith() method call. However, doing so would prevent us from using the fluid API in which the ContinueWith() statements are chained together one after the other. Furthermore, this would force us to deeply embed error-handling logic into the control flow rather than simply relying on exception handling.

+   2. We can surround each delegate body with a try/catch block so that no exceptions go unhandled from the task. Unfortunately,

![](bbox=[0.9, 0.57, 1.0, 0.59])