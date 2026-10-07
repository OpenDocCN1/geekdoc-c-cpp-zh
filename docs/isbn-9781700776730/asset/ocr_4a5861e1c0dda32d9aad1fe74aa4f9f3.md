```
class Derived : public Base {
  protected:
    int mult;
  public:
    Derived(int x, int y) : Base(x), mult(y) {}
    virtual int getValue() { return value * mult; }
};

int main() {
  Base *bptr;
  bptr = new Base(10);
  cout << "Value = " << bptr->getValue() << endl;
  delete bptr;

  bptr = new Derived(10, 2);
  cout << "Value = " << bptr->getValue() << endl;
  delete bptr;
  return 0;
}
```

The keyword virtual informs the compiler that calls to getValue() are to be linked at runtime. The addresses of the two getValue() member functions are stored in an internal table. When statements call virtual member functions, C++ looks up the correct function address from this table. We'll talk more about this later. But if you think this lookup action takes time, you are correct. Using virtual member functions might reduce the program's performance (two extra lookups) although in practice serious slowdowns are rare.

The output produced by the above program is:

```
value = 10
value = 20
```

Now compare the two output statements above. They are exactly identical! So how can they produce different output? We now have enough information to answer this question. The addressed objects determine for themselves which of the two virtual getValue() member functions to call. The decision is made by the program at runtime and not at compile time.

Note that once we declare a function to be virtual in a class, any subclass that declares the same function with the same prototype is also considered a virtual function. Keep in mind that late binding makes sense in C++ only