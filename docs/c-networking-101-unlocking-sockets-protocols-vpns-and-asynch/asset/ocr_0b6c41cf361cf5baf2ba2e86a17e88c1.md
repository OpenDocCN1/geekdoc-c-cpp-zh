# Create TCP Server and Client

Let us start with creating a simple TCP server and client using Boost.Asio library, as it is one of the most popular C++ libraries for network programming.

# Creating a Simple TCP Server

The server waits for a client to connect, reads data sent by the client, and then sends a response back.

Below is a basic TCP server that echoes whatever it receives from a client:

```
#include

using boost::asio::ip::tcp;

int main()

{
```