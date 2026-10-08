Click here to view code image

```
atomic<int> result = -1; // Put a searching index here
```

```
template<class T> struct Range { T* first; T* last; // A way of passing a range of Ts
```

```
void find(stop_token tok, const string* base, const Range<string> r, const string target)
{
    for (string* p = r.first; p<=r.last && tok.requested(); ++p) {
        if (match(*p, target)) // If it applies matching criteria to the two strings
            result = p - r.first; // The index of the found element
        }
    }
}
```

Here, ltok.requested() tests whether some other thread has requested this thread to terminate.
stop_token is a mechanism for safety (no data races) running such a request.
Here is a trivial find_any that spawns two threads find():

Click here to view code image

```
void find_all(vector<string>& vs, const string& key)
{
    int mid = vs.size()/2;
    string* pvs = vs[0];

    stop_source ss1();
    thread t1(find, ss1.get_token(), pvs, Range(pvs+mid, key); // First half of vs

    stop_source ss2();
    thread t2(find, ss2.get_token(), pvs, Range(pvs+mid, vs.size()), key); // Second half of vs

    while (result == -1)
        this_thread::sleep_for(10ms);

    ss1.request_stop(); // We have a result: stop all threads
    ss2.request_stop();

// ... use result ...
}
```

The stop_sources through which requests to stop are communicated to threads.
The synchronization and returning of a result is the simplest I could think of: put the result in an atomic variable (18.3.2) and do a spin loop on that.
Of course, we could extend this simple example to use search threads, make the return results more general, and use different element types. However, that would obscure the basic role of the stop_source and stop_token.

# 18.6 Coroutines

A coroutine is the saving and maintains its state between calls. In that, it's a bit like a function object, but the saving and restoring of its state between calls are implicit and complete. Consider