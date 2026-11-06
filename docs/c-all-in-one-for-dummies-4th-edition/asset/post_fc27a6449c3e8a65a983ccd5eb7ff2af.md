
## FRIENDS OF A SAME CLASS

An instance of a class can access the private and protected members of other instances of the same class. The compiler allows you to do it. However, you normally want objects to remain isolated from each other for all sorts of reasons, including keeping bugs at bay and reducing security risks. It helps to think of the only situation in which this kind of activity is actually useful as a host and client, when one instance acts as a host to a client instance for something like creating a container for an object of the same type. To make this sort of access happen, you provide a pointer to another instance of the same class (the client) inside the host class, perhaps passed in as a parameter. The host class is free to modify any of the passed class members.

```
  Protected
  Private From Peeks
  Protected
  Protected
  Private From FriendFunction
```

## Using Classes and Types within Classes

Sometimes an application needs a fairly complex internal structure to get its work done. Three ways to accomplish this goal with relatively few headaches are nesting classes, embedding classes, and declaring types within classes. The following sections discuss the two most common goals: nesting classes and declaring types within classes. The “Nesting a class” section also discusses protection for embedded classes.

### Nesting a class

You may have times when you create a set of classes with one class acting as the primary class while all the other classes function as supporting classes. For example, you may be a member of a team of programmers, and your job is to write a set of classes that log on to a competitor’s computer at night and lower all the prices on the products. Other members of your team will use your classes in their applications. You’re just writing a set of classes; the teammates are writing the rest of the application. The following sections consider the issues involved in performing this task, as well as a potential solution in the form of nested classes.

### Considering the nesting scenario issues

In the classes you’re creating, you want to make the task easy on your coworkers. In doing so, you may make a primary class, such as `EthicalCompetition`, that they will instantiate to use your set of classes. This primary class will include the methods for using the system. In other words, it serves as an *interface* to the set of classes.

In addition to the main `EthicalCompetition` class, you might create additional auxiliary classes that the `EthicalCompetition` class will use, but your coworkers won’t interact with directly. One might be a class called `Connection` that handles the tasks of connecting to the competitor’s computer. However, the `Connection` class may present these problems:

- **Potential conflicts:** The class `Connection` may be something you write, but your organization may support another `Connection` class, and your coworkers might need to use that class.
- **Privacy:** You may not want your coworkers using this special `Connection` class. Perhaps it has special functionality that would reveal too many organizational secrets, or you just want them using the main interface, the `EthicalCompetition` class.

To solve the unique name problem, you have several choices. For one, you can just rename the class something different, such as `EthicalCompetitionConnection`. But that’s a bit long for a class used exclusively for internal needs. However, you could shorten the class name and call it something that’s likely to be unique, such as `ECConnection`.

Yet at the same time, if the users of your classes look at the header file and see a whole set of classes, which classes they should be using may not be clear. (Of course, you would write some documentation to clear this up, but you do want the code to be at least somewhat self-explanatory.)

### Understanding the nested class solution

One solution for dealing with both naming conflict and privacy issues for support classes is to use *nested classes*. With a nested class, you write the declaration for the main class, `EthicalCompetition`, and then, inside the class, you write the supporting classes, as in the following:

```cpp
class EthicalCompetition {
private:
    class Connection {
    public:
        void Connect();
    };
public:
    void HardWork();
};
```

Note that this shows a class inside a class. Here’s the code for the functions:

```cpp
void EthicalCompetition::HardWork() {
    Connection c;
    c.Connect();
    cout << "Connected" << endl;
}

void EthicalCompetition::Connection::Connect() {
    cout << "Connecting..." << endl;
}
```

The header for the Connect function in the Connection class requires first the outer class name, then two colons, then the inner class name, then two colons again, and finally the function name. This follows the pattern you normally use where you put the class name first, then two colons, and then the function name. But in this case, you have two class names separated with two colons.

When you want to declare an instance of the Connection class, you do it differently, depending on where you are in the code when you declare it:

- **Inside a method of the outer `EthicalCompetition` class:** You simply refer to the class by its name, `Connection`. Look at the method `HardWork`, with this line:

    ```cpp
    Connection c;
    ```
- **Outside the methods:** You can declare an instance of the inner class, `Connection`, without an instance of the outer class, `EthicalCompetition`. To do this, you fully qualify the class name, like this:

    ```cpp
    EthicalCompetition::Connection myconnection;
    ```

This line would go, for instance, in the `main()` function of your application if you want to create an instance of the inner class, `Connection`.

However, you may recall that one of the reasons for putting the class inside the other was to shield it from the outside world, to keep your nosy coworkers from creating an instance of it. But so far, what you’ve done doesn’t really stop them. By declaring the inner class after the outer class, you can now employ the second trick. The idea is to write the inner class so that only the outer class can access the members. To accomplish this task, you make all the members of the inner class either private or protected and then make the outer class, `EthicalCompetition`, a friend of the inner class, `Connection`. Here’s the modified version of the `Connection` class:

```cpp
class EthicalCompetition::Connection {
protected:
    friend class EthicalCompetition;
    void Connect();
};
```

Only the outer class can access most of the `Connection` members now. However, even though the members are protected, nothing stops users outside `EthicalCompetition` from creating an instance of the `Connection` class. To add this security, you employ the third trick, which is to create a constructor for the class that is either private or protected. When you change the constructor’s access, following suit with a destructor is a good idea. Make the destructor private or protected, too. Even if the constructor and destructor don’t do anything, making them private or protected prevents others from creating an instance of the class — others, that is, except any friends to the class. So here’s yet one more version of the class:

```cpp
class EthicalCompetition::Connection {
protected:
    friend class EthicalCompetition;
    void Connect();
    Connection() { }
    ~Connection() { }
};
```

This third trick completes the process. When someone tries to make an instance of the class outside `EthicalCompetition` (such as in `main()`), as in this:

```cpp
EthicalCompetition::Connection myconnect;
```

you see the following message:

```text
'EthicalCompetition::Connection::~Connection()' is protected
```

You can still create an instance from within the methods of `EthicalCompetition`. The ProtectingEmbedded example, shown in Listing 4-5, contains the final application.
