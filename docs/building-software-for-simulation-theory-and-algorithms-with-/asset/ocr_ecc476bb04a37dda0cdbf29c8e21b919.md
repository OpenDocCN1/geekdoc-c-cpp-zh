Nonetheless, every instance of the class should have the same set of input and output variables, and so defining them as class wide constants is a reasonable thing to do.

# N1 Model

```
```cpp
#ifndef _n1_h_
#define _n1_h_
#include "adtss.h"
#include "n2.h"
#include "xor_memory_models.h"

class N1: public adtss::Network<port_value_t>
{
public:
  static const int x1, x2; // Labels for input ports
  // Create the network; components set their own initial state
  N1():adtss::Network<port_value_t>(),
  n2(new N2()) {}
  // Get the set of components in this network
  void getComponents(adtss::Set<adtss::Atomic<port_value_t>*> & c)
  {
    c.insert(&n2);
  }
  }
  // Route input and output within the network
  void route(const port_value_t& value,
    adtss::Atomic<port_value_t>* src,
    adtss::Bag<adtss::Event<port_value_t> > & r)
  {
    adtss::Event<port_value_t> e;
    e.value = value;
    // Input to the network
    if (src == getResultant()) {
      e.model = &n2;
      r.insert(e);
    }
    // Output from N2
    else if (src == &n2) {
      // Output from the network
      e.model = getResultant();
      r.insert(e);
      // Input to M
      e.model = &m;
      r.insert(e);
    }
    // Output from M
    else if (src == &m) {
```
```