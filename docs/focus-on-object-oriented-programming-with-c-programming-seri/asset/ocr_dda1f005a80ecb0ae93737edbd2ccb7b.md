```
cout << num << val << endl; // 5 5
```

Because both variables point to the same location in memory, they are in fact the same variable and therefore output the same value. Note that unlike pointers, reference variables are automatically dereferenced when they are used. There is therefore no need for the asterisk *.

```
++num;
cout << num << val << endl; // 6 6
+val;
cout << num << val << endl; // 7 7
```

Any assignment made to num is reflected through val and any assignment made to val is reflected through num. Any operation on val has precisely the same effect as an operation on num.

```
int z = 100;
val = z;
cout << num << val << endl; // 100 100
```

This does not cause val to refer to z since the compiler always dereferences the address for you. The above code will copy the value of z into num.

Note: Once a reference variable is initialized to some existing value, it cannot be changed or reassigned to some other variables as long as the reference variable remains in scope. However, the value the reference variable points to can always change.

# Rule of References

When a reference variable is created, it must always be initialized with the name of some other existing variable. That means that references must be initialized in their declarations:

```
int& iref; // error
```