
```cpp
class User {

private:

std::string name; // Accessible only within the class

int id; // Accessible only within the class

public:

User(std::string userName, int userId) : name(userName), id(userId) {}

// Public method to access private data

void displayUserInfo() const {

std::cout << "User Name: " << name << ", User ID: " << id <<
std::endl;

}

// Setter and Getter for name - Demonstrating controlled access

void setName(std::string userName) {

    if (!userName.empty()) {

        name = userName;

    }

    // Additional validation or modification logic can go here

}

std::string getName() const {

    return name;

}

// Note: Similar setter and getter methods can be implemented for 'id'

};
```

In this improved version of the User class, both the name and id attributes are marked as private, meaning they cannot be accessed directly from outside the class. This encapsulation ensures that the User objects' states can only be modified through a controlled interface—here, represented by the setName and getName methods, and any other methods you choose to expose publicly. This approach not only safeguards the data from unintended access and modification but also allows for validation and processing within the setter methods, ensuring that the object always remains in a valid state.

### Understanding Access Modifiers

- Private: Members declared as private are accessible only within the class itself. Use this for data and methods that should not be exposed to the outside.
- Protected: Members declared as protected are accessible within the class, by derived classes, and by friend classes. This is less restrictive than private but more so than public, offering a balance between accessibility and protection.
- Public: Members declared as public are accessible from any part of the program. Use this for methods and properties that need to be accessed freely, like interfaces to your class.

You may ensure that your objects remain in a consistent state and reduce the likelihood of defects by selectively making some elements of your class public, protected, or private. Our growing application exemplifies how secure, robust, and maintainable object-oriented software development is built upon encapsulation and the prudent use of access modifiers.

## Recipe 7: Declare and Call Static Members and Methods

### Situation

For example, suppose we'd like to know how many User objects the "GitforGits" app has generated. This tally does not pertain to any particular user, but rather to the class User as a whole. To accomplish this, we can make use of static members, which allow us to create a variable at the class level that is shared by all instances. Furthermore, it would be helpful to have a class-level method that can be used to retrieve the total number of users, for example, instead of having to create a User object. To do this, we can use static methods to work with static data or execute operations that are important to classes.

### Practical Solution

Static members and methods in a class are shared among all instances of that class, acting at the class level rather than the instance level. This feature of object-oriented programming in C++ is particularly useful for scenarios where you want to maintain a piece of data consistently across all objects of a class or invoke functionality without necessarily having an instance of the class. In the context of our application, static members could be used to track global states or

```cpp
public:

User(std::string userName) : name(userName) {

userCount++; // Increment user count whenever a new User object is
created

}

~User() {

userCount--; // Decrement user count when a User object is destroyed

}

static int getUserCount() { // Static method to access the user count

return userCount;

}

void displayUserInfo() const {

std::cout << "User Name: " << name << std::endl;

}
```

In the above given code snippet, userCount is a static member variable of the User class, initialized to 0. Every time a User object is created, the constructor increments and every time a User object is destroyed, the destructor decrements it. The static method getUserCount provides access to this count without needing an instance of

### Understanding Static Members

Static Member Variables: Shared across all instances of the class. They are useful for representing data that is common to all objects of that class.

Static Methods: Can be called without an instance of the class. They can only access static members or other static methods.

Static members and methods are accessed using the class name and the scope resolution operator as shown with This emphasizes that these members belong to the class itself rather than to any instance of the class. This capability is invaluable in situations where you need to maintain global state or provide utilities related to a class in your "GitforGits" application.

## Recipe 8: Create Friend Functions and Friend Classes

### Situation

There may be times when the application needs to grant access to secret and protected members of another class to an external function or class. In situations like this, knowing how friend functions and classes work is crucial. Using these C++ capabilities, trusted non-member functions or classes can break the encapsulation restrictions in a controlled manner and access a class's secret and protected areas. With careful use of these features, you can perform activities that need access to a class's internals without making them public.

### Practical Solution

### Understanding Static Members

Static members of a class in C++ are shared across all instances of the class. They belong to the class itself rather than any object instance and can be accessed without creating an instance of the class. Static members are useful for storing class-wide information, and static methods can access only static members.

### Implementing Friend Functions and Friend Classes

```cpp
#include

#include

class User;

class UserLogger {

public:

static void logUserInfo(const User& user);

};

class User {

private:

std::string name;

int id;

// Declaring a friend function

friend void displayUserInfo(const User& user);

// Declaring a friend class

friend class UserLogger;

public:

User(std::string userName, int userId) : name(userName), id(userId) {}

};

// Friend function definition

void displayUserInfo(const User& user) {

    std::cout << "User Name: " << user.name << ", User ID: " << user.id
    << std::endl;

}

// Friend class method definition

void UserLogger::logUserInfo(const User& user) {

    std::cout << "[LOG] User Name: " << user.name << ", User ID: " <<
    user.id << std::endl;

}

int main() {

    User alice("Alice", 1);

    displayUserInfo(alice); // Direct access to private members of User

    UserLogger::logUserInfo(alice); // Access through a friend class

    return 0;

}
```

In the above given sample program, displayUserInfo is a non-member function that has been granted access to the User class's private members via the friend keyword, allowing it to read private data and display user information. Similarly, UserLogger is a friend class that has a static method which also accesses the private data of This setup demonstrates how friend functions and classes can interact closely with a class while maintaining the encapsulation of its members from the rest of the program.

### Key Takeaway

Friend functions and classes are powerful tools for specific scenarios where direct access to a class's private or protected members is justified. Use these features sparingly and thoughtfully, as they can compromise encapsulation and make code maintenance more challenging by creating tight coupling between classes or functions.
