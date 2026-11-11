```
~~~java
Process last = processes.get(processes.size() - 1);
var result = new String(last.getInputStream().readAllBytes());
~~~
```

Of course, this particular task would be more efficiently solved by making the directory walk in Java instead of running four processes. Chapter 2 of Volume II will show you how to do that.

# ### 12.8.2 Running a Process

After you have configured the builder, invoke its start method to start the process. If you configured the input, output, and error streams as pipes, you can now write to the input stream and read the output and error streams. For example,

```
~~~java
Process process = new ProcessBuilder("/bin/ls", "-l")
    .directory(Path.of("/tmp").toFile())
    .start();
try (var in = new Scanner(process.getInputStream())) {
    while (in.hasNextLine())
        System.out.println(in.nextLine());
}
~~~
```

> > **CAUTION:** There is limited buffer space for the process streams. You should not flood the input, and you should read the output promptly. If there is a lot of input and output, you may need to produce and consume it in separate threads.

To wait for the process to finish, call

```
~~~java
int result = process.waitFor();
~~~
```

or, if you don't want to wait indefinitely,

```
~~~java
long delay = . . .;
if (process.waitFor(delay, TimeUnit.SECONDS)) {
    int result = process.exitValue();
} else {
    process.destroyForcibly();
}
~~~
```

The first call to waitFor returns the exit value of the process (by convention, 0 for success or a nonzero error code). The second call returns true if the process didn't time out. Then you need to retrieve the exit value by calling the exitValue method.

Instead of waiting for the process to finish, you can just leave it running and occasionally call isAlive to see whether it is still alive. To kill the process,