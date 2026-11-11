```
```cpp
}

private:
    StreamSocket socket;
    SocketReactor& reactor;
};

class DataHandler {
public:

    DataHandler(StreamSocket& s, SocketReactor& r): socket(s), reactor(r),
        outFile("reactorOutput.txt") {
        reactor.addEventHandler(socket,
            Observer<DataHandler, ReadableNotification>(*this, &DataHandler::socketReadable));
        reactor.addEventHandler(socket,
            Observer<DataHandler, ShutdownNotification>(*this, &DataHandler::socketShutdown));
        socket.setBlocking(false);
    }

    ~DataHandler() {
        reactor.removeEventHandler(socket,
            Observer<DataHandler, ReadableNotification>(*this, &DataHandler::socketReadable));
        reactor.removeEventHandler(socket,
            Observer<DataHandler, ShutdownNotification>(*this, &DataHandler::socketShutdown));
    }

    void socketReadable(ReadableNotification*) {
        char buffer[64];
        int n = 0;
        do {
            n = socket.receiveBytes(&buffer[0], sizeof(buffer));
            if (n > 0) {
                std::string s(buffer, n);
                outFile << s << std::flush;
            }
            else break;
        } while (true);
    }

    void socketShutdown(ShutdownNotification*) {
        delete this;
    }

private:
    StreamSocket socket;```
```