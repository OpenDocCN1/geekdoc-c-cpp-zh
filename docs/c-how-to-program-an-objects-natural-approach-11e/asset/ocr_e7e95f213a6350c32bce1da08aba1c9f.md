We now have the object files `deitel.math.o` and `deitel.math-impl.o` representing the module's interface and implementation. Finally, compile the main application and link it with `deitel.math.o` and `deitel.math-impl.o`:

```
```bash
g++ -fmodules-ts fig16_08.cpp deitel.math.o deitel.math-impl.o
             -o fig16_08
```
```

# ### Compiling This Example in clang++

In clang++, use the commands from Section 16.6.6 to compile the standard library headers `<algorithm>`, `<iostream>`, `<iterator>`, `<numeric>` and `<vector>` as header units. Next, compile the primary module interface unit into a precompiled module (`.pcm`) file:

```
```bash
clang++ -std=c++20 -fmodule-file=vector.pcm
        -x c++-module deitel.math.ixx --precompile -o deitel.math.pcm
```
```

Next, compile the module implementation unit into an object file:

```
```bash
clang++ -std=c++20 -fmodule-file=deitel.math.pcm
        -fmodule-file=vector.pcm -fmodule-file=numeric.pcm
        -c deitel.math-impl.cpp -o deitel.math-impl.o
```
```

The option `-fmodule-file=deitel.math.pcm` specifies the name of the module's primary module interface unit. Finally, compile the main application and link it with the files `deitel.math-impl.o` and `deitel.math.pcm`:

```
```bash
clang++ -std=c++20 -fmodule-file=algorithm.pcm
        -fmodule-file=iostream.pcm -fmodule-file=iterator.pcm
        -fmodule-file=vector.pcm fig16_08.cpp deitel.math-impl.o
        -fprebuilt-module-path=. deitel.math.pcm -o fig16_08
```
```

# ### 16.8.2 Example: Modularizing a Class

Let's define a simplified version of Chapter 9's `Time` class with its interface in a **primary module interface unit** and its implementation in a **module implementation unit**. We'll name our module `deitel.time` and place the class in the `deitel::time` namespace.

# ### deitel.time Primary Module Interface Unit

The `deitel.time` module's primary module interface unit (Fig. 16.9) defines and exports the namespace `deitel::time` (lines 7–19) containing the `Time` class definition (lines 8–18).

```
```cpp
1   // Fig. 16.9: deitel.time.ixx
2   // Primary module interface for a simple Time class.
3   export module deitel.time; // declare the primary module interface
4
5   import <string>; // rather than #include <string>
6
7   export namespace deitel::time {
8       class Time {
9       public:
10          // default constructor because it can be called with no arguments
11          explicit Time(int hour = 0, int minute = 0, int second = 0);
12
13          std::string toString() const;
```
```

![](bbox=[0.178, 0.887, 0.595, 0.902])