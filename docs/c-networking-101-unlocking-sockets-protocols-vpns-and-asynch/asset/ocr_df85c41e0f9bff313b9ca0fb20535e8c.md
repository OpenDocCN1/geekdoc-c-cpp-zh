```
if (result < 0) {
    std::cerr << "Failed to set SO_BROADCAST!" <<
    std::endl;

    return 1;

}

return 0;

}
```

In the above sample program, we're doing two things:

For a TCP socket, we're enabling the TCP_NODELAY option. This option disables Nagle's algorithm, which is a TCP feature that attempts to automatically improve efficiency by buffering small packets and sending them together. Disabling it might improve performance for certain applications that want to send out small packets immediately.