```
```cpp
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
```