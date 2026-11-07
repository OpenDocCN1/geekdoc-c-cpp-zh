```
```cpp
boost::beast::flat_buffer buffer;

http::response res;

http::read(socket, buffer, res);

std::cout << res << std::endl;

socket.shutdown(tcp::socket::shutdown_both);

}

catch (std::exception const& e)

{

    std::cerr << "Error: " << e.what() << std::endl;

    return EXIT_FAILURE;

}

return EXIT_SUCCESS;

}
```
```