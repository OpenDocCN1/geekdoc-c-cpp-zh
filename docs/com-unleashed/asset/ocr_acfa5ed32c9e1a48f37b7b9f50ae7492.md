If your object reaches a state in which it is definitely done with its part of the transaction, the object can request deactivation from MTS. As a result, the object will also be destroyed. Remember that the transaction does not end until the root object is deactivated. However, when a subordinate object is destroyed, the object notifies the application that it has completed voting. To deactivate itself, an object can call one of two methods in the `IObjectContext` interface: `SetComplete()` or `SetAbort()`. `SetComplete()` and `SetAbort()` tell MTS that the object has completed doing its job.

In other words, when the method call finishes and passes through the context wrapper, MTS will deactivate the context wrapper and destroy the object. `SetComplete()` tells MTS that it wants to be deactivated in a happy state; `SetAbort()` tells MTS that it wants to be deactivated in an unhappy state. Deactivation occurs when the call returns through the context wrapper. The following code demonstrates calling the `SetComplete()` method:

```
IObjectContext *pContext;
HRESULT hr = GetObjectContext(&pContext);
if (SUCCEEDED(hr))
{
    pContext->SetComplete();
    pContext->Release();
}
```

> **Note**
> 
> In COM+, the object will have a choice to be destroyed or pooled. Based on the previous rules for voting, you can infer the following rules:
> 
> - If an object says that it is unhappy with DisableCommit, it can change its mind and become happy with EnableCommit. An object can change its mind until it is destroyed.
> - If one object calls SetAbort within a method call and does not change its mind—ending the method call with SetComplete, for example—when the call ends and goes through the context wrapper, MTS will destroy the object, and the transaction will be doomed.
> - If the root object is destroyed, any objects that are part of the transaction will also be destroyed.

# Designing with MTS

Many developers like to call SetAbort() at the beginning of the method code, and then call SetComplete() when they are sure that the code has executed properly. In this way, if an unexpected error occurs and the method exits prematurely, changes will not be committed.