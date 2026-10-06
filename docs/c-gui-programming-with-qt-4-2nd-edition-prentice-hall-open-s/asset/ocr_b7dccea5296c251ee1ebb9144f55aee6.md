```
void Thread::run()
{
    while (!stopped) {
        std::cerr << QPrintable(messageStr);
        stopped = false;
        std::cerr << std::endl;
    }
}
```

The run() function is called to start executing thread. As long as the stopped variable is false, the function keeps printing the given message to the console. The Thread terminates when control leaves the run() function.

```
void Thread::stop()
{
    stopped = true;
}
```

The stop() function sets the stopped variable to true, thereby telling run() to stop printing text to the console. This function can be called from any thread at any time. For the purposes of this example, we assume assignment to a bool is an atomic operation. This is a reasonable assumption, considering that a bool can have only two states. We will see later in this section how to use QMutex to guarantee that assignment to a variable is an atomic operation.

Thread provides a terminate() function that terminates the execution of the thread while it is still running. Using terminate() is not recommended, since it can stop the thread at any point and not give the thread any chance to clean up after itself. It is always safer to use a stopped variable and a stop() function as we did here.

We will now show how to use the Thread class in a small Qt application that uses two threads, A and B, in the main thread.

```
class ThreadDialog : public QDialog
{
    Q_OBJECT

public:
    ThreadDialog(QWidget parent = 0);

protected:
    void closeEvent(QCloseEvent event);
```