```
```cpp
DoAccept();

}

private:

void DoAccept() {

    acceptor_.async_accept(

        [this](boost::system::error_code ec, tcp::socket socket) {

            if (!ec) {

                std::make_shared(std::move(socket))->Start();

            }

            DoAccept();

        });

}

tcp::acceptor acceptor_;
```
```