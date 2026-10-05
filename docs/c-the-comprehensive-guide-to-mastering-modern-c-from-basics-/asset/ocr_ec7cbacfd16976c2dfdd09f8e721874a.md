to override and use methods, then use overload to ensure you are really overriding.

The normal implementation using a member would look like the following listing. The (base) Engine class remains unchanged.

```
// https://godbolt.org/z/67EjhMf54
class Car {
public:
    Car() : engine_{8} {} // initializes a car with 8 cylinders
    void start() { engine_.start(); } // starts the car by starting the engine
private:
    Engine engine_; // Car has-a Engine
};
```

# Listing 18.8 Has-a relationship using a member.

The commonalities of both implementations are as follows:

+   - In both cases, there is exactly one Engine in each Car instance.
- In neither case can users of the Car* class convert into an Engine*, as would be the case with public inheritance.
- In both examples, Car has a start() method that leads to a call to the start() method of the contained motor.

However, there are also differences. For the inheritance variant, the following applies:

+   - You cannot choose this if Car is supposed to contain multiple Engine instances.
- Members of Car can convert a car* into an Engine*.