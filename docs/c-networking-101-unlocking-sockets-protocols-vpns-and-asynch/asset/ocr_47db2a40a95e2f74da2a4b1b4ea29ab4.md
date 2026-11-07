```
```cpp
{

boost::asio::io_service io_service;

tcp::resolver resolver(io_service);

tcp::resolver::query query("localhost", "1234");

tcp::resolver::iterator endpoint_iterator =
resolver.resolve(query);

tcp::socket socket(io_service);

boost::asio::connect(socket, endpoint_iterator);

std::string message = "Hello from client!";

boost::system::error_code ignored_error;

boost::asio::write(socket,
boost::asio::buffer(message), ignored_error);

char reply[1024];
```
```