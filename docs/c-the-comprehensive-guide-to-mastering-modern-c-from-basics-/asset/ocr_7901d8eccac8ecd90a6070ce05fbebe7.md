```
int MyValue::counter = 0; // initialization of the static class
variable
```

# Listing 16.3 A destructor is executed when an object is removed.

Equipped like this, you can use the object as usual. To do this, use specific variables of this modified MyValue type in Listing 16.1.

```
// https://gdbbolt.org/z/enneOEwPzb
void function(const MyValue &paramRef) {
  MyValue localValue("local");
}

int main() {
  MyValue mvalue1("mvalue1");
  function( MyValue{\{"temp" });
  function( mvalue1) {
    MyValue mvalue2("mvalue2");
  }
}
```

# Listing 16.4 Here, many objects are created and destroyed.

Thus, you get the output shown in the following listing.

+   Constructor mvalue1
Constructor temp
Constructor local
Destructor local
Destructor temp
Constructor local
Destructor local
Constructor mvalue2
Destructor mvalue2
Destructor mvalue1

# Listing 16.5 This output shows when objects are created and destroyed.