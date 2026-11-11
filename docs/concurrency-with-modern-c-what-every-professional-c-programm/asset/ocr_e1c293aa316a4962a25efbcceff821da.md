```
```cpp
90  tcp::socket socket;
91 };

93 class DataServer {
94 public:
95   DataServer(asio::io_context& io_context, short port, const std::string& file)
96       : acceptor_(io_context, tcp::endpoint(tcp::v4(), port)),
97         socket_(io_context), fileName(file) {
98     do_accept();
99   }

101 private:
102   void do_accept() {
103     acceptor_.async_accept(socket_,
104       [this](std::error_code error_code) {
105         std::make_shared<DataSession>(std::move(socket_), std::move(fileName))->start();
106         do_accept();
107       });
108   }

110   tcp::acceptor acceptor_;
111   tcp::socket socket_;
112   std::string fileName;
113 };

116 int main() {

118   asio::io_context io_context;
119   EchoServer echoServer(io_context, 4711);
120   DataServer dataServer(io_context, 4712, "proactorOutput.txt");
121   io_context.run();

122 }
```
```

The program uses an EchoServer (line 118) and a DataServer, listening to the specified Ports 4711 and 4712. The EchoServer writes the incoming data back, and the DataServer writes them into the file proactorOutput.txt.

The EchoServer accepts in the member function do_accept (line 80) client’s requests and handles them using EchoSession (line 13). do_accept is recursively called (line 84). When a client request is made. The crucial parts of the EchoSession are the member functions do_read (line 22) and do_write (line 30). do_read reads the data from the client connection asynchronously (line 24) and do_write writes them asynchronously (line 32) back. In the end, the member function do_write calls do_read (line 34) to read all incoming client data.