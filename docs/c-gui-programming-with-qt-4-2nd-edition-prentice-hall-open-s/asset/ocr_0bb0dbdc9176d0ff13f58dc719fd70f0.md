this, SIGNAL(updateRecord(const QString));

When the first signal is emitted, the second signal is emitted as well. Apart from that, signal-slot connections are indistinguishable from signal-slot connections.

+   Connections can be removed:

```
disconnect(lcd, SIGNAL(overflow()),
      this, SLOT(handleError()));
```

This is rarely needed, because Qt automatically removes all connections involving an object when that is deleted.

To connect a signal to a slot (or to another signal), they must have the same parameter types in the same order:

```
connect(ftp, SIGNAL(rawCommandReply(int, const QString)),
      this, SLOT(processReply(int, const QString));
```

Exceptionally, if a signal has more parameters than the slot it is connected to, the additional parameters are simply ignored:

```
connect(ftp, SIGNAL(rawCommandReply(int, const QString)),
      this, SLOT(checkErrorCode(int));
```

If the parameter types are incompatible, or if the signal or slot doesn't exist, Qt will issue a warning at run-time if the application is built in debug mode. Similarly, Qt will give a warning if parameter names are included in the signal or slot signatures.

So far, we have only used signals and slots with widgets. But the mechanism itself is implemented in QObject and isn't limited to GUI programming. The mechanism can be used by any QObject subclass:

```
class Employee : public QObject
{
    Q_OBJECT

public:
    Employee() { mySalary = 0; }

    int salary() const { return mySalary; }
```