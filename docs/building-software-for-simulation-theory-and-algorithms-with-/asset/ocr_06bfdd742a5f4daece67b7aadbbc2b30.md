```
```cpp
41            e.model = &m;
42            r.insert(e);
43        }
44        // Output from M
45        else if (src == &m) {
46            // Input to N2
47            e.model = &n2;
48            e.value.port = N2::m;
49            r.insert(e);
50        }
51    }
52    private:
53        N2 n2;
54        Memory m;
55 };
56
57 #endif
```
```

# ## Revised N2 Model

```
```cpp
1 #ifndef n2_h
2 #define n2_h
3 #include "adts.h"
4 #include "xor_memory_models.h"
5
6 class N2: public adts::Network<port_value_t>
7 {
8     public:
9         static const int m, x1, x2;
10
11        N2():adts::Network<port_value_t>(),
12            xor1(),xor2()
13        {
14            xor1.setParent(this);
15            xor2.setParent(this);
16        }
17
18        void getComponents(adts::Set<adts::Dtss<port_value_t>*>& c)
19        {
20            c.insert(&xor1);
21            c.insert(&xor2);
22        }
23
24        void route(const port_value_t& value, adts::Dtss<port_value_t>* src,
25            adts::Bag<adts::Event<port_value_t> >& r)
26        {
27            adts::Event<port_value_t> e;
28            e.value = value;
29            // Input to the network
```
```