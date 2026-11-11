To build this application, first compile the `com.horstmann.greet` module:

```
```bash
javac -d com.horstmann.greet/module-info.java \\
    com.horstmann.greet/com/horstmann/greet/Greeter.java \\
    com.horstmann.greet/com/horstmann/greet/internal/GreeterImpl.java
```
```

Then compile the application module with the first module on the module path:

```
```bash
javac -p com.horstmann.greet v2ch09.exportedpkg/module-info.java \\
    v2ch09.exportedpkg/com/horstmann/hello/HelloWorld.java
```
```

Finally, run the program with both modules on the module path:

```
```bash
java -p v2ch09.exportedpkg:com.horstmann.greet \\
    -m v2ch09.exportedpkg/com.horstmann.hello.HelloWorld
```
```

> **TIP:** To build this application with Eclipse, make a separate project for each module. In the `v2ch09.exportedpkg` project, edit the project properties. In the Projects tab, add the `com.horstmann.greet` module to the module path—see Figure 9.2.

![](bbox=[0.139, 0.504, 0.774, 0.844])

**Figure 9.2** Adding a dependent module to an Eclipse project