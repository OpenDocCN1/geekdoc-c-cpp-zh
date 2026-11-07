```
```cpp
// invokes the String(const String &) constructor
String * favorite = new String(sayings[choice]);
```
```

+   - You use the `->` operator to access a class method via a pointer:
+     ```cpp
+     if (sayings[i].length() < shortest->length())
+     ```

+   - You apply the dereferencing operator (`*`) to a pointer to an object to obtain an object:
+     ```cpp
+     if (sayings[i] < *first)  // compare object values
+         first = &sayings[i];  // assign object address
+     ```

| Description | Example |
|---|---|
| Declaring a pointer to a class object: | `String * glamour;` |
| Initializing a pointer to an existing object: | `String * first = &sayings[0];` |
| Initializing a pointer using `new` and the default class constructor: | `String * gleep = new String;` |
| Initializing a pointer using `new` and the `String(const char*)` class constructor: | `String * glop = new String("my my my");` |
| Initializing a pointer using `new` and the `String(const String &)` class constructor: | `String * favorite = new String(sayings[choice]);` |
| Using the `->` operator to access a class method via a pointer: | `if (sayings[i].length() < shortest->length())` (annotations: `object`; `pointer to object`) |
| Using the `*` dereferencing operator to obtain an object from a pointer: | `if (sayings[i] < *first)` (annotations: `object`; `pointer to object`) |

Figure 12.5  Pointers and objects.