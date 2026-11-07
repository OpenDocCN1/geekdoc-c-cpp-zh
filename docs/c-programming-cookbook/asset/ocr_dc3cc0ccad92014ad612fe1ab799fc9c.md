# # Implementing Friend Functions and Friend Classes

We shall consider an enhanced version of the User class where we want to implement a functionality that allows an external function and class to access its private data. This could be useful for operations like serialization, where an external utility needs to access an object's state without altering the class's public interface.

```
```cpp
#include

#include

class User;

class UserLogger {

public:

static void logUserInfo(const User& user);

};
```
```