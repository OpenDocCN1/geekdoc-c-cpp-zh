no distinction between deactivation and destruction, except that the context wrapper is still available in the deactivation phase.) COM+ introduces the concept of object pooling, in which an object can control whether releasing all references truly deletes the object, or whether the object is instead stored in an object pool.

To implement IObjectControl for receiving JIT notifications, do the following:

+   1. Add IObjectControl to the inheritance list of your MTS-compatible class.
+   2. Add the interface to your query interface map as follows:
+      `COM_INTERFACE_ENTRY(IObjectControl)`
+   3. Implement the three methods in IObjectControl—Activate, CanBePooled, and Deactivate.

```
HRESULT Ctestobj1::Activate()
{
}

BOOL Ctestobj1::CanBePooled()
{
    return FALSE;
}
void Ctestobj1::Deactivate()
{
}
```

Object pooling is not available in MTS 2; therefore, the previous code should return FALSE.

> **Note**
> 
> In reality, you can also return TRUE. Some people suggest answering TRUE so that object pooling can start working as soon as it is available. However, this is not recommended unless the implications of object pooling have been carefully considered.

# Creating Packages to Host Components

After you have created your middle-tier components, you will want to create packages to host your components.

To create a package in MTS, do the following:

+   1. In MTS Explorer, open the Computers branch.
+   2. Open the computer branch where you want the package to be installed.