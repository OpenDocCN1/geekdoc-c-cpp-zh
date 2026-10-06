Providing multiple threads in a Qt application is straightforward: We just subclass QThread and reimplement its run() function. To show how this works, we will start by reviewing the code for a very simple QThread subclass that repeatedly prints a string on a console. The application's user interface is shown in Figure 14.1.

```
class Thread : public QThread
{
    Q_OBJECT

public:
    Thread();

    void setMessage(const QString &message);
    void stop();

protected:
    void run();

private:
    QString messageStr;
    volatile bool stopped;
};
```

# Figure 14.1. The Threads application

![](bbox=[0.01, 0.522, 0.325, 0.602])

The Thread class is derived from QThread and reimplements the run() function. it provides two additional functions: setMessage() and stop().

The stopped variable is declared volatile because it is accessed from different threads and we want to be sure that it is freshly read every time it is needed. If we omitted the volatile keyword, the compiler might optimize access to the variable, possibly leading to incorrect results.

```
Thread::Thread()
{
    stopped = false;
}
```

We set stopped to false in the constructor.