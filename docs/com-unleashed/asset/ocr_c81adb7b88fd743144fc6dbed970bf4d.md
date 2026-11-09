**LISTING 5.2 Continued**

```
```cpp
    pMoniker->Release();
    return punknown;
}

int main()
{
    ::CoInitialize(NULL);
    IUnknown * pu = CreateAndBind(L"e:\\old.doc");
    pu->Release();
    ::CoUninitialize();

    return 0;
}
```
```

# ### IMoniker::BindToStorage()

The `IMoniker::BindToStorage()` method retrieves an instance to the storage interface (usually `IStorage` or `IStream` interfaces) for the moniker. This does not load an instance of the implementation COM object.

# ### IMoniker::ComposeWith()

The `IMoniker::ComposeWith()` method creates a new composite moniker from this moniker and another moniker. This moniker is considered to be the left moniker in the composite.

For a description of composite monikers, see the “Composite Monikers” section later in this chapter.

# ### IMoniker::Enum()

The `IMoniker::Enum()` method retrieves an instance of the `IEnumMoniker` object for the composite moniker. The `IEnumMoniker` object can be used to enumerate the component monikers of the composite.

# ### IMoniker::IsEqual() and IMoniker::Reduce()

The `IMoniker::IsEqual()` method determines whether two monikers are equal. Call the `IMoniker::Reduce()` method before calling the `IMoniker::IsEqual()` method to reduce the moniker to its most specific form.

# ### IMoniker::Hash()

The `IMoniker::Hash()` method returns a `DWORD`. The `DWORD` can be used by other components to bucket sort monikers.

![](bbox=[0.886, 0.735, 1.0, 0.897])