```
```cpp
}

// useStaticLocal initializes static local variable x only the
// first time the function is called; value of x is saved
// between calls to this function
void useStaticLocal() {
    static int x{50}; // initialized first time useStaticLocal is called

    cout << "\nlocal static x is " << x << " on entering useStaticLocal"
         << endl;
    ++x;
    cout << "local static x is " << x << " on exiting useStaticLocal"
         << endl;
}

// useGlobal modifies global variable x during each call
void useGlobal() {
    cout << "\nglobal x is " << x << " on entering useGlobal" << endl;
    x *= 10;
    cout << "global x is " << x << " on exiting useGlobal" << endl;
}
```
```

```
```text
global x in main is 1
local x in main's outer scope is 5
local x in main's inner scope is 7
local x in main's outer scope is 5

local x is 25 on entering useLocal
local x is 26 on exiting useLocal

local static x is 50 on entering useStaticLocal
local static x is 51 on exiting useStaticLocal

global x is 1 on entering useGlobal
global x is 10 on exiting useGlobal

local x is 25 on entering useLocal
local x is 26 on exiting useLocal

local static x is 51 on entering useStaticLocal
local static x is 52 on exiting useStaticLocal

global x is 10 on entering useGlobal
global x is 100 on exiting useGlobal

local x in main is 5
```
```

Fig. 6.11 Scoping example.