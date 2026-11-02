```
```cpp
// Garbage collection method does not do anything
void gc_output(adtss::Bag<port_value_t>&){}
private:
    bool s;
};

// Definition of the memory machine
class Memory: public adtss::Atomic<port_value_t>
{
    public:
        Memory():adtss::Atomic<port_value_t>()
        {
            s[0] = s[1] = false;
        }
        // State transition function
        void delta(const adtss::Bag<port_value_t>& xb)
        {
            // Make sure the input bag is acceptable
            assert(xb.size() == 1);
            // Process the input
            s[0] = s[1];
            s[1] = (*(xb.begin())).bit;
        }
        // Output function
        void output_func(adtss::Bag<port_value_t>& yb)
        {
            port_value_t output;
            output.bit = s[0];
            yb.insert(output);
        }
        // Garbage collection method does not do anything
        void gc_output(adtss::Bag<port_value_t>&){}
    private:
        bool s[2];
};

#endif
```
```

The code for *N₁* and *N₂* is listed next. *N₁* contains the *Resultant* that contains the network *N₂*, not *N₂* itself; *N₁* puts this *Resultant* into its set of components and uses it to route events. Classwide (i.e., static) constants that implement the models’ input ports are another feature of the classes that implement the networks. If the ports are constant, there is no risk that they will be accidentally overwritten and cause obscure, difficult-to-find errors. By making them classwide variables (i.e., static) we can ensure that the memory used by the simulation is reduced. This is a small advantage, and the model must be large before it yields any real benefits.