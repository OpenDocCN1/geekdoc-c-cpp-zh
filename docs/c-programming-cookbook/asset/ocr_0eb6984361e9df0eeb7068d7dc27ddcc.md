```
```cpp
std::cout << "Fetching user data..." << std::endl;

// Wait for the coroutine to complete and get the result

std::cout << futureUserData.get() << std::endl;

return 0;

}
```
```

In the above given code snippet, fetchUserData is a coroutine that simulates an asynchronous operation using co_return to provide the result. The future returned from the coroutine can be used to wait for the operation to complete and to retrieve the result.

# Benefits of Using Coroutines

Coroutines make asynchronous code look and behave more like synchronous code, improving its readability.

By allowing functions to pause and resume, coroutines enable non-blocking operations, keeping your application responsive.

Writing asynchronous code without coroutines often involves nested callbacks or complex state machines. Coroutines abstract away these complexities.