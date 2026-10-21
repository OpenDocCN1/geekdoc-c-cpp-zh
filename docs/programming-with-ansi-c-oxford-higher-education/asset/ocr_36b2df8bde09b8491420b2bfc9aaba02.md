```
cout << "Shape pointer to Circle pointer casted\n";
else
cout << "Shape pointer to Circle pointer not casted\n";
/* A derived pointer pointing to derived is casted to base */
PtrShape = dynamic_cast<Shape *> (&Ring);
if(PtrShape)
cout << "Circle pointer to Shape pointer casted\n";
else
cout << "Circle pointer to Shape pointer not casted\n";
/* Part II */
/* Casting from base class pointer to derived */
/* A base pointer pointing to a derived class object
is casted to a derived class object successfully */
cout << "Trying to cast a base class pointer\n";
cout << "pointing to a derived class object\n";
cout << "to a derived class pointer\n";
PtrShape = &Ring;
PtrCircle = dynamic_cast<Circle *> (PtrShape);
if(PtrCircle)
cout << "Successful\n";
else
cout << "Unsuccessful\n";
/* A base pointer pointing to a base class object
failed to cast to a derived class object */
cout << "Trying to cast a base class pointer\n";
cout << "pointing to a base class object\n";
cout << "to a pointer to a derived class object\n";
PtrShape = &SomeShape;
PtrCircle = dynamic_cast<Circle *> (PtrShape);
if(PtrCircle)
cout << "Successful\n";
else
cout << "Unsuccessful\n";
/* A derived pointer pointing to a derived object
is casted to a base class pointer successfully */
cout << "Trying to cast a derived class pointer\n";
cout << "pointing to a derived class object\n";
cout << "to a base class pointer\n";
PtrCircle = &Ring;
PtrShape = dynamic_cast<Shape *> (PtrCircle);
if(PtrShape)
cout << "Successful\n";
else
cout << "Unsuccessful\n";
/* The only option left is a derived class pointer
pointing to a base class object, which is not possible */
```

Output
Shape pointer to Shape pointer casted
Circle pointer to Circle pointer casted