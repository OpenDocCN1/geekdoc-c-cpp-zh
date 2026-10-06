QStack<T> QQueue<T> are two examples of convenience subclasses.
Stack<T> provides push(), pop(), top(). QQueue<T> provides enqueue(), dequeue(), head().

For all the containers seen so far, the value type T can be a basic type like int or double, a pointer, or a class that has a default constructor (a constructor that takes no arguments), a copy constructor, and an assignment operator. Classes that qualify include ByteArray, QDateTime, QRegExp, QString, and QVariant that are derived from QObject do not qualify, because they lack a copy constructor and an assignment operator. This is no problem in practice, since we can simply store pointers to QObject rather than the objects they represent.

The value type T can also be a container, in which case we must remember to separate consecutive angle brackets with spaces; otherwise, the compiler will choke on what it thinks is a >> operator. For example:

```
QList<QVector<double> > list;
```

In addition to the types just mentioned, a container's value type can be any class that meets the criteria described earlier. Here is an example of such a class:

```
class Movie
public:
    Movie(const QString &title = = "", int duration = 0);
    void setTitle(const QString &title) { myTitle = title; }
    QString title() const { return myTitle; }
    void setDuration(int duration) { myDuration = duration; }
    QString duration() const { return myDuration; }

private:
    QString myTitle;
    int myDuration;
};
```

The class has a constructor that requires no arguments (although it can take up to two). It also has a copy constructor and an assignment operator, both implicitly provided by C++. For this class, a member-by-member copy is sufficient, so there is no need to implement our own copy constructor and assignment operator.

Qt provides two categories of iterators for traversing the items stored in a