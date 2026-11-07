```
```cpp
}

void server(boost::asio::io_service& io_service, short
port) {

    tcp::acceptor a(io_service, tcp::endpoint(tcp::v4(),
port));

    for (;;) {

        tcp::socket sock(io_service);

        a.accept(sock);

        std::thread(session, std::move(sock)).detach();

    }

}

int main(int argc, char* argv[]) {
```
```