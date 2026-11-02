```
```cpp
// Confluent event otherwise
else (*iter).m->delta_conf(xb);
// Reset the elapsed time
(*iter).e = 0.0;
}
// otherwise, does it have input?
else if (!xb.empty()) {
    (*iter).m->delta_ext((*iter).e + time_adv,xb);
    (*iter).e = 0.0;
}
// just update the elapsed time otherwise
else (*iter).e += time_adv;
}
}

template <typename X>
void Result<X>::delta_ext(double e, const Bag<X>& xb)
{
    // Send the input to the proper components
    for (typename Bag<X>::const_iterator iter = xb.begin();
            iter != xb.end(); iter++)
        route(*iter,this);
    // Compute next state of each component
    for (typename std::vector<total_state_t>::iterator iter = c.begin();
            iter != c.end(); iter++) {
        // Get the bag of input for the model
        Bag<X>& xb = input[(*iter).m];
        // Update the elapsed time
        (*iter).e += e;
        // If it has input, apply the external transition function
        if (!xb.empty()) {
            (*iter).m->delta_ext((*iter).e,xb);
            (*iter).e = 0.0;
        }
    }
}
}

template <typename X>
void Result<X>::delta_conf(const Bag<X>& xb)
{
    // Send the input to the proper components
    for (typename Bag<X>::const_iterator iter = xb.begin();
            iter != xb.end(); iter++)
        route(*iter,this);
    // The confluent transition is the same as the internal transition
    // when the network inputs have been routed to their destinations
    delta_int();
}
```
```