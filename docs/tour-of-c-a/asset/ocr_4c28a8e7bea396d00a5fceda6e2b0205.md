```
pmr::synchronized_pool_resource pool; // make a pool
struct Event {
    vector<int> data = vector<int>{512,&pool}; // let Events use the pool
}
list<shared_ptr<Event>> q {&pool}; // let q use the pool
```