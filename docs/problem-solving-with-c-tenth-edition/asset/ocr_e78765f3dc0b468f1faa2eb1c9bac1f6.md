# DISPLAY 15.13 More Inheritance with Virtual Functions (part 2 of 2)

```
46      // << pPet->breed << endl;
47      //generates an error message: 'class Pet' has no member
48      //named 'breed' .
49      //See Pitfall section "Not Using Virtual Member Functions"
50      //for more discussion on this.
51
52      return 0;
53  }
54
55  void Dog::print()
56  {
57      cout << "name: " << name << endl;
58      cout << "breed: " << breed << endl;
59  }
60
61  void Pet::print()
62  {
63      cout << "name: " << endl;//Note no breed mentioned
64  }
```

# Sample Dialogue

```
name: Tiny
breed: Great Dane
name: Tiny
breed: Great Dane
```

# PITFALL The Slicing Problem

Although it is legal to assign a derived class object to a base class variable, assigning a derived class object to a base class object slices off data. Any data members in the derived class object that are not also in the base class will be lost in the assignment, and any member functions that are not defined in the base class are similarly unavailable to the resulting base class object.

If we make the following declarations and assignments:

```
Dog vDog;
Pet vPet;
vDog.name = "Tiny";
vDog.breed = "Great Dane";
vPet = vDog;
```

then vPet cannot be a calling object for a member function introduced in Dog, and the data member, Dog::breed, is lost.