# Solutions to Chapter 13 | C++

13.7 Why does a destructor in base class need to be declared virtual? pg 76

# SOLUTION

Calling a method with an object pointer always invokes:

+   >> the most derived class function, if a method is virtual.

+   >> the function implementation corresponding to the object pointer type (used to call the method), if a method is non-virtual.

A virtual destructor works in the same way. A destructor gets called when an object goes out of scope or when we delete on an object pointer.

When any derived class object goes out of scope, the destructor of that derived class gets called first. Then it calls its parent class destructor so memory allocated to the object is properly released.

But, if we delete an object on a base pointer which points to a derived class object, the base class destructor gets first (for non-virtual function). For example:

```
class Base {
  public:
  Base() { cout << "Base Constructor " << endl; }
  ~Base() { cout << "Base Destructor " << endl; } /* see below */
};
class Derived: public Base {
  public:
  Derived() { cout << "Derived Constructor " << endl; }
  ~Derived() { cout << "Derived Destructor " << endl; }
};
void main() {
  Base *p = new Derived();
  delete p;
}
```

Output:
Base Constructor
Derived Constructor
Base Destructor

If we declare the base class destructor as virtual, this makes all the derived class destructors virtual as well. Note this thing about being ordered into the v-table.

If we replace the above destructor with:

```
virtual ~Base() {
  cout << "Base Destructor" << endl;
}
```