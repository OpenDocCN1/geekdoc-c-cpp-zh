```
    std::cout << "Current Status: " << currentStatus << std::endl;

    // Another identifier named OK in the same scope
    int OK = 42;

    // Attempting to use the same identifier for a different purpose
    std::cout << "Another OK." << OK << std::endl;

    return 0;
    }
```

In this example, the enum constants OK and ERROR share the same scope as the surrounding code. However, this can lead to unintended naming clashes, as demonstrated by the introduction of another identifier with the same name.

# ## Scoped Enums for Enhanced Encapsulation

To mitigate naming conflicts and enhance encapsulation, C++ introduces scoped enums, also known as enum class. Scoped enums encapsulate their constants within a distinct scope, preventing them from polluting the surrounding namespace. Here's an example:

```
    #include <iostream>

    // Scoped enum named ConnectionState
    enum class ConnectionState {
        CONNECTED,
        DISCONNECTED
    };

    int main() {
        // Using ConnectionState enum to declare a variable
        ConnectionState currentConnection = ConnectionState::CONNECTED;

        // Displaying the current connection state
        std::cout << "Current Connection State: " << static_cast<int>(currentConnection) <<
            std::endl;

        // No risk of naming conflicts with a different identifier named CONNECTED
        int CONNECTED = 42;

        // Safely using the identifier for a different purpose
        std::cout << "Another CONNECTED: " << CONNECTED << std::endl;

        return 0;
    }
```