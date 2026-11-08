```
```cpp
// If you forgot this, you would have a memory leak. If you used
// 'delete' instead of 'delete[]' unknown bad things might happen. Some
// implementations will do ...
// knows what else.
delete[] p_ArrInt;
p_ArrInt = nullptr;

wcout << L"Ending program." << endl;
return 0;
}
```
```

For whom it is inconvenient to run the sample, here is the output I get when I run this from a command prompt on Windows 8 Release Preview, compiled with Visual Studio 2012 Ultimate RC in Debug configuration targeting the x86 chipset. You will probably produce different values for the addresses and thread IDs if you run it on your own system.

```
```
Creating SomeClass instance.
StringId: s_someClass.
Address is: '0x009fade8'.
Value is '10'.
Thread id: '3660'.

Creating SomeClass instance.
StringId: g_staticSomeClass.
Address is: '0x013f8554'.
Value is '20'.
Thread id: '3660'.

Creating SomeClass instance.
StringId: __pmain sc1.
Address is: '0x007bfe98'.
Value is '1'.
Thread id: '3660'.

sc1 value: '1'.

Creating SomeClass instance.
StringId: __pmain sc2.
Address is: '0x007bfe70'.
Value is '2'.
Thread id: '3660'.

sc2 value: '2'.

Destroying SomeClass instance.
StringId: __pmain sc2.
Address is: '0x007bfe70'.
```
```