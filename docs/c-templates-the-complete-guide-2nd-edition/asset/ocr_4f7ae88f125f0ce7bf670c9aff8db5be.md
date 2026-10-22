```
template<typename T>
class Creator {
    friend void feed(Creator<T>) { // every T instantiates a different function ::feed()
        ...
    }
};

int main()
{
    Creator<void> one;
    feed(one);                     // instantiates ::feed(Creator<void>)
    Creator<double> two;
    feed(two);                     // instantiates ::feed(Creator<double>)
}
```