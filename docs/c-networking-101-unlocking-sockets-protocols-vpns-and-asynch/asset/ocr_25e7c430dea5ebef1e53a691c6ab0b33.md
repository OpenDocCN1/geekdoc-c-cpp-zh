```
```cpp
void Start() {
    DoRead();
}

private:

void DoRead() {
    auto self(shared_from_this());

    socket_.async_read_some(boost::asio::buffer(data_,
    max_length),
        [this, self](boost::system::error_code ec,
        std::size_t length) {
            if (!ec) {
                DoWrite(length);
            }
```
```