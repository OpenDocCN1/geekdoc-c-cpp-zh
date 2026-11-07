The client connects to the server, sends some data, and reads the server's response.

Below is a simple TCP client that sends a message to the server and prints the server's response:

```
```cpp
#include

#include

using boost::asio::ip::tcp;

int main()
{
    boost::asio::io_service io_service;

    tcp::resolver resolver(io_service);

    tcp::resolver::query query("localhost", "1234");

    tcp::resolver::iterator endpoint_iterator = resolver.resolve(query);

    tcp::socket socket(io_service);

    boost::asio::connect(socket, endpoint_iterator);
```
```