```
Vector<string> vs {"Hello", "World"};      // OK: Vector<string>
Vector vs1 = {"Hello", "World"};             // OK: deduces to Vector<const char*> (Surprise!)
Vector vs2 = {"Hello",s", "World"s};             // OK: deduces to Vector<string>
Vector vs3 = {"Hello",s", "World"};             // error: the initializer list is not homogenous
Vector<string> vs4 = {"Hello",s", "World"};     // OK: the element type is explicit
```