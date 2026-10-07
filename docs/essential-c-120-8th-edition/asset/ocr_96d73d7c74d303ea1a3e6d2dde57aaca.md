# Chapter 23: Platform Interoperability and Unsafe Code

bytes. The type specified before the * is the referent type—that is, the type located where the value of the pointer refers. In this example, pData is the pointer and byte is the referent type, as shown in Figure 23.1.

![](bbox=[0.268, 0.209, 0.702, 0.333])

Figure 23.1: Pointers contain the address of the data

Because pointers are simply integers that happen to refer to a memory address, they are not subject to garbage collection. C# does not allow refer types other than unmanaged types, which are types that are not reference types, are not generics, and do not contain reference types. Therefore, the following command is not valid:

```
string* pMessage;
```

Likewise, this command is not valid:

```
ServiceStatus* pStatus;
```

where ServiceStatus is defined as shown in Listing 23.13. The problem, once again, is that ServiceStatus includes a string field.

Listing 23.13: Invalid Referent Type Example

```
struct ServiceStatus
{
    int State;
    string Description; // Description is a reference type
}
```