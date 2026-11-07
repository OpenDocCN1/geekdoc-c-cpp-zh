```
```cpp
#include

namespace http = boost::beast::http;

namespace net = boost::asio;

namespace ssl = net::ssl;

using tcp = net::ip::tcp;

int main()

{

try

{

auto const host = "example.com";

auto const port = "443";

auto const target = "/index.html";

int version = 11;

net::io_context ioc;
```
```