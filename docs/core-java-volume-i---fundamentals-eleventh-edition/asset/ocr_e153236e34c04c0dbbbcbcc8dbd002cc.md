# 8.6.9 You Can Defeat Checked Exception Checking

A bedrock principle of Java exception handling is that you must provide a handler for all checked exceptions. You can use generics to defeat this scheme. The key ingredient is this method:

```
```java
@SuppressWarnings("unchecked")
static <T extends Throwable> void throwAs(Throwable t) throws T
{
    throw (T) t;
}
```
```

Suppose this method is contained in an interface Task. When you have a checked exception e and call

```
```java
Task.<RuntimeException>throwAs(e);
```
```

then the compiler will believe that e becomes an unchecked exception. The following turns all exceptions into those that the compiler believes to be unchecked:

```
```java
try
{
    do work
}
catch (Throwable t)
{
    Task.<RuntimeException>throwAs(t);
}
```
```

Let’s use this to solve a vexing problem. To run code in a thread, you have to place it into the run method of a class that implements the Runnable interface. But that method is not allowed to throw checked exceptions. We will provide an adaptor from a Task, whose run method is allowed to throw arbitrary exceptions, to a Runnable:

```
```java
interface Task
{
    void run() throws Exception;

    @SuppressWarnings("unchecked")
    static <T extends Throwable> void throwAs(Throwable t) throws T
    {
        throw (T) t;
    }

    static Runnable asRunnable(Task task)
    {
        return () ->
        {
```
```