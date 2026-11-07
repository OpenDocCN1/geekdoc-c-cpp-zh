```
```cpp
using boost::asio::ip::tcp;

int main() {

  try {

    boost::asio::io_service io_service;

    tcp::acceptor acceptor(io_service,
tcp::endpoint(tcp::v4(), 12345));

    for (;;) {

      tcp::socket socket(io_service);

      acceptor.accept(socket);

      std::array<char, 128> buf;

      boost::system::error_code error;

      while (true) {

        size_t len =
socket.read_some(boost::asio::buffer(buf), error);
```
```