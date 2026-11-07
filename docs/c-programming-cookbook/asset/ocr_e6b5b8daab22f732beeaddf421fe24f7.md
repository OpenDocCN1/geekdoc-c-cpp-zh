```
```cpp
#include

class User {

private:

std::string name;

int id;

public:

// Constructor

User(std::string userName, int userId) : name(userName), id(userId) {}

// Method to display user information

void displayUserInfo() const {

std::cout << "User Name: " << name << ", User ID: " << id <<
std::endl;
```
```