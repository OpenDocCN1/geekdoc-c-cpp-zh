```
~~~cpp
char data_[max_length];

};

class server

{

public:

  server(boost::asio::io_context& io_context, short port)

    : io_context_(io_context),

      acceptor_(io_context, tcp::endpoint(tcp::v4(), port))

  {

    start_accept();

  }

  void start_accept()
~~~
```