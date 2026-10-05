```
class VwBus : public Car {;
class ModelT : public Car {;

void letDrive(Car vehicle) { // Value parameter copies only base
class
void letBrake(Car &vehicle) { // Reference parameter
void letHonk(Car *vehicle) { // Passed as pointer
int main() {
    VwBus bus {}; // automatic variable
    Car *modelT = new ModelT( }; // dynamically managed
    letDrive(bus); // gets copied to Car
    letDrive(*modelT); // gets copied to Car
    letBrake(bus); // remains VwBus
    letBrake(*modelT); // remains ModelT
    letHonk(&bus); // remains VwBus
    letHonk(modelT); // remains ModelT
}
```

# Listing 19.1 Call-by-reference as a basis for polymorphism.

Because the parameter is defined as a value parameter in letDrive(), C++ copies using the copy constructor. And the responsibility for how to copy lies with the object that is needed within letDrive()—and that is a Car. So it is the copy constructor of the Car class that is used here. But it only knows how to copy Car, not VwBus or ModelT.

However, if you pass a reference into a function like letBrake(), nothing needs to be copied, so the vehicle remains exactly the type it was outside.

Specifying the parameter as a pointer is somewhat similar to a reference. Here, only the pointer itself is the value parameter and is copied upon entering the letHonk function. The object itself, bus or modelT, remains the same.