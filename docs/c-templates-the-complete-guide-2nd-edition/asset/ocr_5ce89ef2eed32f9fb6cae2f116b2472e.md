```
template<>
class Danger<void> {
    public:
        enum { max = 100 };
};

void clear(char* buf)
{
    // mismatch in array bound:
    for (int k = 0; k<Danger<void>::max; ++k) {
        buf[k] = '\0';
    }
}
```