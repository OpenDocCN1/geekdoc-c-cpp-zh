```
```cpp
boost::asio::placeholders::error,
boost::asio::placeholders::bytes_transferred));
}
else
{
delete this;
}
}
private:
tcp::socket socket_;
enum { max_length = 1024 };
```
```