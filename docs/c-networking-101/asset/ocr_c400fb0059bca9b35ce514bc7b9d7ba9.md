```
```cpp
using namespace std;

mapHWAddress<6>> ips;

bool callback(const PDU& pdu) {

  const ARP &arp = pdu.rfind_pdu();

  ips[arp.sender_ip_addr()] = arp.sender_hw_addr();

  return true;

}

int main() {

  SnifferConfiguration config;

  config.set_promisc_mode(true);

  config.set_filter("arp");

  Sniffer sniffer("eth0", config);

  sniffer.sniff_loop(callback);

}
```
```