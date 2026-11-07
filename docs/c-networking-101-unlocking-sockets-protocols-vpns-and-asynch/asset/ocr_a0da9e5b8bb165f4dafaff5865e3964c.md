```
```cpp
size_t reply_length = boost::asio::read(socket,
boost::asio::buffer(reply,1024), ignored_error);

std::cout << "Reply is: ";

std::cout.write(reply, reply_length);

std::cout << "\n";

return 0;

}
```
```

In this code:

+   - `tcp::resolver::query` is used to specify the server's address and port number.

`tcp::socket` is used to create a socket and `boost::asio::connect` to connect it to the server.

+   - It then sends a message to the server and waits for a response.