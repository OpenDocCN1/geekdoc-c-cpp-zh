then pressing *Enter*.

```
```bash
~$ cd examples/ch01
~/examples/ch01$
```
```

**Fig. 1.20 Changing to the `GuessNumber` application’s directory.**

# *Step 2: Compiling the Application*

Before running the application, you must first compile it (**Fig. 1.21**) by typing

```
```bash
g++ -std=c++14 GuessNumber.cpp -o GuessNumber
```
```

This command compiles the application for C++14 (the current C++ version) and produces an executable file called `GuessNumber`.

```
```bash
~/examples/ch01$ g++ -std=c++14 GuessNumber.cpp -o GuessNumber
~/examples/ch01$
```
```

**Fig. 1.21 Compiling the GuessNumber application using the `g++` command.**

# *Step 3: Running the Application*