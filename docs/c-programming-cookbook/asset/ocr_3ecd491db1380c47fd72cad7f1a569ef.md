```
    public:

    UserNotFoundException(const std::string& username)

    : GitforGitsException("User not found: " + username),
    username(username) {},

    const std::string& getUsername() const { return username; }

    private:

    std::string username;

    };

    // Usage in application code

    void findUser(const std::string& username) {

    // Simulate user not found

    throw UserNotFoundException(username);

    }
```