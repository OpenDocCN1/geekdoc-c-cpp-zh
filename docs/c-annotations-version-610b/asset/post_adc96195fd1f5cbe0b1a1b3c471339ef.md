
### 13.5 Redefining member functions

Derived classes may redefine base class members. Let's assume that a vehicle classification system must also cover trucks, consisting of two parts: the front part, the tractor, pulls the rear part, the trailer. Both the tractor and the trailer have their own mass, and the mass function should return the combined mass.

The definition of a `Truck` starts with a class definition. Our initial `Truck` class is derived from `Auto` but it is then expanded to hold one more `size_t` field representing the additional mass information. Here we choose to represent the mass of the front part of the truck in the `Auto` class and to store the mass of the trailer in an additional field:

```cpp
class Truck: public Auto
{
    size_t d_trailer_mass;

public:
    Truck();
    Truck(size_t tractor_wt, size_t speed, char const *name,
          size_t trailer_wt);

    void setMass(size_t tractor_wt, size_t trailer_wt);
    size_t mass() const;
};

Truck::Truck(size_t tractor_wt, size_t speed, char const *name,
             size_t trailer_wt)
:
    Auto(tractor_wt, speed, name)
{
    d_trailer_mass = trailer_wt;
}
```

Note that the class `Truck` now contains two functions already present in the base class `Auto`: `setMass` and `mass`.

- The redefinition of `setMass` poses no problems: this function is simply redefined to perform actions which are specific to a `Truck` object.
- Redefining `setMass`, however, *hides* `Auto::setMass`. For a `Truck` only the `setMass` function having two `size_t` arguments can be used.
- The `Vehicle`'s `setMass` function remains available for a `Truck`, but it must now be called *explicitly*, as `Auto::setMass` is hidden from view. This latter function is hidden, even though `Auto::setMass` has only one `size_t` argument. To implement `Truck::setMass` we could write:

    ```cpp
    void Truck::setMass(size_t tractor_wt, size_t trailer_wt)
    {
        d_trailer_mass = trailer_wt;
        Auto::setMass(tractor_wt);    // note: Auto:: is required
    }
    ```

- Outside of the class `Auto::setMass` is accessed using the scope resolution operator. So, if a `Truck` truck needs to set its `Auto` mass, it must use

    ```cpp
    truck.Auto::setMass(x);
    ```

```cpp
cout << '\n' << "Truck weighs " <<
             lorry.Vehicle::mass() << '\n' <<
       "Truck + trailer weighs " << lorry.mass() << '\n' <<
       "Speed is " << lorry.speed() << '\n' <<
       "Name is " << lorry.name() << '\n';
}
```

The class `Truck` was derived from `Auto`. However, one might question this class design. Since a truck is conceived of as a combination of a tractor and a trailer it is probably better defined using composition. This changes our point of view from a `Truck` being an `Auto` (and some strangely appearing data members) to a `Truck` consisting of an `Auto` (the tractor) and a `Vehicle` (the trailer). `Truck`’s interface is now very specific, not requiring users to study `Auto`’s and `Vehicle`’s interfaces and it opens up possibilities for defining ‘road trains’: tractors towing multiple trailers. Here is an example of such an alternate class setup:

```cpp
class Truck
{
    Auto d_lorry;
    Vehicle d_trailer;        // use vector<Vehicle> for road trains

public:
    Truck();
    Truck(size_t tractor_wt, size_t speed, char const *name,
          size_t trailer_wt);

    void setMass(size_t tractor_wt, size_t trailer_wt);
    void setTractorMass(size_t tractor_wt);
    void setTrailerMass(size_t trailer_wt);
    size_t mass() const;
    size_t tractorMass() const;
    size_t trailerMass() const;
    // consider:
    Auto const &tractor() const;
    Vehicle const &trailer() const;
};
```

### 13.6 iostream::init

Consider classes derived from `std::istream` or `std::ostream`. Such a class could be designed as follows:

```cpp
class XIstream: public std::istream
{
public:
    ...
};
```

Assuming that the `streambuf` to which `XIstream` interfaces is not yet available at construction time, `XIstream` only offers default constructors. The class could, however, offer a member `void switchStream(std::streambuf *sb)` to replace `XIstream` objects with a `streambuf` interface to. How to implement `switchStream`?

The classes `std::istream` and `std::ostream` offer a protected member `void init(std::streambuf *sb)` to realize this. The init member expects a pointer to a streambuf which is associated with the istream or ostream object. The init member properly ends any existing association before switching to the streambuf whose address is provided to init.

Assuming that the `streambuf` to which `switchStream`’s `sb` points persists, then `switchStream` could simply be implemented like this:

```cpp
void switchStream(streambuf *sb)
{
    init(sb);
}
```

### 13.7 Multiple inheritance

Up to now, a class has always been derived from a single base class. In addition to single inheritance C++ also supports *multiple inheritance*. In multiple inheritance a class is derived from several base classes and hence inherits functionality from multiple parent classes at the same time.

When using multiple inheritance it should be defensible to consider the newly derived class an instantiation of both base classes. Otherwise, composition is more appropriate. In general, linear derivation (using only one base class) is used much more frequently than multiple derivation. Good class design dictates that a class should have a single, well described responsibility and that principle often conflicts with multiple inheritance where we can state that objects of class `Derived` are *both* `Base1` *and* `Base2` objects.

But then, consider *the prototype* of an object for which multiple inheritance was used to its extreme: the *Swiss army knife*! This object is a knife, it is a pair of scissors, it is a can-opener, it is a corkscrew, it is ....

The ‘Swiss army knife’ is an extreme example of multiple inheritance. In C++ there *are* some good reasons, not violating the ‘one class, one responsibility’ principle that is covered in the next chapter. In this section the technical details of constructing classes using multiple inheritance are discussed.

How to construct a ‘Swiss army knife’ in C++? First we need (at least) two base classes. For example, let’s assume we are designing a toolkit allowing us to construct an instrument panel of an aircraft’s cockpit. We design all kinds of instruments, like an artificial horizon and an altimeter. One of the components that is often seen in aircraft is a *nav-com set*: a combination of a navigational beacon receiver (the ‘nav’ part) and a radio communication unit (the ‘com’-part). To define the nav-com set, we start by designing the `NavSet` class (assume the existence of the classes `Intercom`, `VHF_Dial` and `Message`):

```cpp
class NavSet
{
    public:
        NavSet(Intercom &intercom, VHF_Dial &dial);

        size_t activeFrequency() const;
        size_t standByFrequency() const;

        void setStandByFrequency(size_t freq);
        size_t toggleActiveStandby();
        void setVolume(size_t level);
        void identEmphasis(bool on_off);
};
```

Next we design the class `ComSet`:

```cpp
class ComSet
{
    public:
        ComSet(Intercom &intercom);

    size_t frequency() const;
    size_t passiveFrequency() const;

    void setPassiveFrequency(size_t freq);
    size_t toggleFrequencies();

    void setAudioLevel(size_t level);
    void powerOn(bool on_off);
    void testState(bool on_off);
    void transmit(Message &message);
};
```

Using objects of this class we can receive messages, transmitted through the Intercom, but we can also *transmit* messages using a Message object that's passed to the ComSet object using its transmit member function.

Now we're ready to construct our NavCom set:

```cpp
class NavComSet: public ComSet, public NavSet
{
    public:
        NavComSet(Intercom &intercom, VHF_Dial &dial);
};
```

Done. Now we have defined a NavComSet which is *both* a NavSet *and* a ComSet: the facilities of both base classes are now available in the derived class using multiple inheritance.

Please note the following:

- The keyword public is present before both base class names (NavSet and ComSet). By default inheritance uses *private derivation* and the keyword public must be repeated before each of the base class specifications. Base classes are not required to use the same derivation type. One base class could have public derivation and another base class could use private derivation.
- The multiply derived class NavComSet introduces no additional functionality of its own, but merely combines two existing classes into a new aggregate class. Thus, C++ offers the possibility to simply sweep multiple simple classes into one more complex class.
- Here is the implementation of the NavComSet constructor:

    ```cpp
    NavComSet::NavComSet(Intercom &intercom, VHF_Dial &dial)
    :
        ComSet(intercom),
        NavSet(intercom, dial)
    {}
    ```

    The constructor requires no extra code: Its purpose is to activate the constructors of its base classes. The order in which the base class initializers are called is *not* dictated by their calling order in the constructor's code, but by the ordering of the base classes in the class interface.

- The NavComSet class definition requires no additional data members or member functions: here (and often) the inherited interfaces provide all the required functionality and data for the multiply derived class to operate properly.

Of course, while defining the base classes, we made life easy on ourselves by strictly using different member function names. So, there is a function setVolume in the NavSet class and a function setAudioLevel in the ComSet class. A bit cheating, since we could expect that both units in fact have a composed object Amplifier, handling the volume setting. A revised class might offer an Amplifier
