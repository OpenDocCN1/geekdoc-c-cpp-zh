```
```cpp
class Composed
{
    Base_d_base;
    ...
};
```
```

Why and when prefer Derived over Composed and vice versa? What kind of inheritance should be used when designing the class Derived?

+   - Since Composed and Derived are offered as alternatives we are looking at the design of a class (Derived or Composed) that *is-implemented-in-terms-of* another class.
+   
+   - Since Composed does itself not make Base’s interface available, Derived shouldn’t do so either. The underlying principle is that *private inheritance* should be used when deriving a class Derived from Base where Derived is-implemented-in-terms-of Base.
+   
+   - Should we use inheritance or composition? Here are some arguments:
+     - In general terms composition results in looser coupling and should therefore be preferred over inheritance.
+     - Composition allows us to define classes having multiple members of the same type (think about a class having multiple `std::string` members) which can not be realized using inheritance.
+     - Composition allows us to separate the class’s interface from its implementation. This allows us to modify the class’s data organization without the need to recompile code using our class. This is also known as the *bridge design pattern* or the *compiler firewall* or *pimpl* (pointer to the implementation) idiom.
+     - If Base offers members in its protected interface that must be used when implementing Derived inheritance must also be used. Again: since we’re implementing-in-terms-of the inheritance type should be private.
+     - Protected inheritance may be considered when the derived class (D) itself is intended as a base class that should only make the members of its own base class (B) available to classes that are derived from it (i.e., D).

Private inheritance should also be used when a derived class is a certain type of base class, but in order to initialize that base class an object of another class type must be available. Example: a new `istream` class-type (say: a stream `IRandStream` from which random numbers can be extracted) is derived from `std::istream`. Although an `istream` can be constructed empty (receiving its `streambuf` later using its `rdbuf` member), it is clearly preferable to initialize the `istream` base class right away.

Assuming that a `Randbuffer: public std::streambuf` has been created for generating random numbers then `IRandStream` can be derived from `Randbuffer` and `std::ostream`. That way the `ostream` base class can be initialized using the `Randbuffer` base class.

As a `RandStream` is definitely not a `Randbuffer` *public inheritance* is not appropriate. In this case `IRandStream` is-implemented-in-terms-of a `Randbuffer` and so *private inheritance* should be used.

IRandStream’s class interface should therefore start like this:

```
```cpp
class IRandStream: private Randbuffer, public std::istream
{
public:
    IRandStream(int lowest, int highest)    // defines the range
    :
        Randbuffer(lowest, highest),
        std::istream(this)                  // passes &Randbuffer
    {}
...
};
```
```