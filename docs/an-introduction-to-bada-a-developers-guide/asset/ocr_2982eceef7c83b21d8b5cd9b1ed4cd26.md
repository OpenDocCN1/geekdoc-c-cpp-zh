```
result r = E_SUCCESS;

// Close socket
r = pSocket->Close();

if(r == E_SUCCESS)
{
    //Release resource
    delete pSocket;
    pSocket = null;
}
```

# Hints, Pitfalls, and Related Topics

An instance of SecureSocket can only be created and used in the asynchronous (non-blocking) mode. It can only be used for the TCP client socket functionality. The secure socket feature of bada supports a CipherSuite mechanism, which is a combination of certain certificate types, ciphers, MACs, key exchange algorithms, and compression methods.

# Recipe 5.3: Establish Normal and Pipeline Connection Modes for HTTP Sessions

# Problem Description

You want to establish HTTP normal and pipeline connection modes.

# The Recipe

The following configuration is required for this recipe:

| Namespaces used: | Osp::Base, Osp::Net::Http, Osp::Net |
| Header files to #include: | FBase.h, FNet.h |
| Required libraries: | FNet |
| Required privilege level: | Normal |
| Required privilege groups: | NET |