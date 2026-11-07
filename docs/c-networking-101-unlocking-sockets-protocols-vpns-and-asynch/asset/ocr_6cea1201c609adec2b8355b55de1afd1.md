```
```cpp
if (result == 0) {

    std::cout << "VPN connection successful." <<
std::endl;

} else {

    std::cout << "Failed to connect VPN." << std::endl;

    return 1;

}

// ... Perform actions while VPN is active ...

// Stop the VPN.

result = system(stopVPNCommand.c_str());

if (result == 0) {

    std::cout << "VPN disconnect successful." <<
std::endl;
```
```