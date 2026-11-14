+   - `-I directory`: Add `directory` to include path;
+   - `-O n`: Optimize with level `n`;
+   - `-g`: Generate debug information;
+   - `-p`: Generate profiling information;
+   - `-o filename`: name the output `filename` instead of `a.out`;
+   - `-c`: Compile only, do not link;
+   - `-D macro`: Define `macro`;
+   - `-L directory`: Add `directory` to the search path for libraries; and
+   - `-l file`: Link with library `lib file.a` or `lib file.so`.

A little more complex example is:

Click here to view code image

```
g++ -o myfluxer myfluxer.cpp -I/opt/include -L/opt/lib -lblas
```

It compiles the file `myfluxer.cpp` and links it with the BLAS library in directory `/opt/lib`. Include files are searched in `/opt/include` in addition to the standard include path. For generating fast executables, we have to use at least the following flags:

```
-O3 -DNDEBUG
```

`-O3` is the highest optimization in `g++`. `-DNDEBUG` defines a macro that lets `assert` disappear in the executable by conditional compilation (`#ifndef NDEBUG`). Disabling assertion is very important for performance: MTL4, for instance, is almost an order of magnitude slower since each access is then range-checked. Conversely, we should use certain compiler flags for debugging as well:

```
-O0 -g
```

`-O0` turns off all optimizations and globally disables inlining so that a debugger can step through the program. The flag `-g` lets the compiler store all names of functions and variables and labels of source lines in the binaries so that a debugger can associate the machine code with the source.