```
~~~cpp
std::array1024> send_buf = { "Hello, World!\n" };

socket.send_to(boost::asio::buffer(send_buf,
send_buf.size()), receiver_endpoint);

std::array1024> recv_buf;

udp::endpoint sender_endpoint;

size_t len =
socket.receive_from(boost::asio::buffer(recv_buf),
sender_endpoint);

std::cout.write(recv_buf.data(), len);

}

catch (std::exception& e) {

std::cerr << e.what() << std::endl;

}
~~~
```