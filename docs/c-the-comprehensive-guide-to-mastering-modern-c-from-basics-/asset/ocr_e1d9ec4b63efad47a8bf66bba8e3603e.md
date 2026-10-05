```
std::cout << "allocate"<<(buf_.size())-current_
<<"current_";
    if(current_ +add > buf_.size()) throw std::bad_alloc();
    char* result = buf_.data()+current_;
    current_ += add;
    return reinterpret_cast<T*>(result);
}
void deallocate(T* p, size_t count) {
    size_t t = sizeof(T)*count;
    std::cout << "deallocate"<<del<<"
"
    if(current== p && reinterpret_cast<T*>(buf_.data())) {
        std::cout << "...all free.\n"
        current_ = 0; // release everything again
    }
}
```

GobAllocator() : GobAllocator(1024)
explicit GobAllocator(size_t mx)
    buf_(mx, 0),
    current_(0) { }

private:
    std::vector<char> buf;
    size_t current_n

```
int main() {
constexpr size_t CNT = 1*1000*1000;
using Gob = GobAllocator<int>;
try {
    Gob gob(sizeof(int)); // prepare allocator
    std::vector<int,Gob> data(gob); // get memory in one go
    data.reserve(CNT);
    for(int val=0; val < (int)CNT; ++val)
        data.push_back(val);
} catch(std::bad_alloc &ex) {
    std::cout << "Memory exhausted.\n"
}
```

# Listing 24.10 A simple allocator and its usage.

The GobAllocator acquires a vector<char> as a memory reservoir upon creation. It can allocate memory when the container requests it via allocate(), but it rarely deallocates it. The container requests this via deallocate(). Only if deallocate() wants to release all the