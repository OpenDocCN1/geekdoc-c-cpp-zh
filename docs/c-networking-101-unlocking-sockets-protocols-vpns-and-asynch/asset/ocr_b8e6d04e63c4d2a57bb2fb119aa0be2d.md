```
int main(int argc, char* argv[])
{
    try
    {
        if (argc != 2)
        {
            std::cerr << "Usage: async_tcp_echo_server \n";
            return 1;
        }
        boost::asio::io_context io_context;
        using namespace std; // For atoi.
        server s(io_context, atoi(argv[1]));
```