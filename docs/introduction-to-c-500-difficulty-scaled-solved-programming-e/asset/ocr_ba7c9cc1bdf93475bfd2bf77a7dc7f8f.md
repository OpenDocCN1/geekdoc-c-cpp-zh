# 17 • Classes and Objects 541

router to which it is connected. It should also contain two numerical members, in order to store the number of packets transmitted by the network card and the number of packets received. You should decide about the access type of the PC members so that the network administrator can safely configure three addresses as well as learn the packet values. A program that tests the functionality of the PC class.

Answer:

```
#include <iostream>
#include <string>
using std::cout;
using std::string;
```

```
class PC {
private:
    string MAC_addr;
    string IP_addr;
    string gateway_IP_addr;
    unsigned int send_pkts; /* In a real implementation, this value increases each time the network card sends a packet. */
    unsigned int rcvd_pkts; /* In a real implementation, this value increases each time the network card receives a packet. */
public:
    PC() {send_pkts = rcvd_pkts = 0};
    void set_MAC_addr(const string& MAC) {MAC_addr = MAC; }
    void set_IP_addr(const string& IP) {IP_addr = IP; }
    void set_gateway_IP_addr(const string& send_pkts) {gateway_IP_addr = IP; }
    unsigned int get_send_pkts() const {return send_pkts;}
    unsigned int get_rcvd_pkts() const {return rcvd_pkts;}
    void show() const;
};
```

```
void PC::show() const {
    cout << "MAC: " << MAC_addr << " IP: " << IP_addr << " Gateway: " << gateway_IP_addr << '\n';
}
```

```
int main() {
    PC pc;
    string s = "1.2.3.4.5.";
    pc.set_MAC_addr(s);
    s = "200.1.2.3";
    pc.set_IP_addr(s);
    s = "200.1.2.1";
    pc.set_gateway_IP_addr(s);
    pc.show();
    cout << "Send: " << pc.get_send_pkts() << " ' "Rcvd: " << pc.get_rcvd_pkts() << '\n';
    return 0;
}
```