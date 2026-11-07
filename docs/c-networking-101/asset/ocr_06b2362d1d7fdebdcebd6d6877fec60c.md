```
```cpp
tcp::acceptor a(io_service, tcp::endpoint(tcp::v4(), port));

for (;;) {
    tcp::socket sock(io_service);

    a.accept(sock);

    std::thread(session, std::move(sock)).detach();

}

}

int main(int argc, char* argv[]) {

    try {

        boost::asio::io_service io_service;

        server(io_service, std::atoi(argv[1]));

    }

    catch (std::exception& e) {

        std::cerr << "Exception: " << e.what() << "\n";
```
```