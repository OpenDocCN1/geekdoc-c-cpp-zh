```
Shape pointer to Circle pointer not casted
Circle pointer to Shape pointer casted
Trying to cast a base class pointer
pointing to a derived class object
to a derived class pointer
Successful
Trying to cast a base class pointer
pointing to a base class object
to a pointer to a derived class object
Unsuccessful
Trying to cast a derived class pointer
pointing to a derived class object
to a base class pointer
Successful
```

# How the Program Works

Note that the derived class to derived class and the base class to base class conversions are obviously acceptable. Look at the following casting operations. Both of them are successful.

```
PtrShape = dynamic_cast<Shape *> (&SomeShape);
PtrCircle = dynamic_cast<Circle *> (&Ring);
```

It can also be seen that the derived class pointer to base class pointer conversion is also acceptable.

```
PtrShape = dynamic_cast<Shape *> (&Ring);
```

Base class pointer to derived class pointer is possible only if base class pointer is actually pointing to a derived class object. So, the following conversion is not successful. Conversion from a Shape pointer to a Circle pointer will fail when the pointer is pointing to a base class object.

```
PtrCircle = dynamic_cast<Circle *> (&SomeShape);
```

However, we will succeed in the following attempt, as the pointer that we are trying to convert is indeed pointing to a derived class.

```
PtrShape = &Ring;
PtrCircle = dynamic_cast<Circle *> (PtrShape);
```

The following is another example where a derived class pointer is casted into a base class pointer successfully. The derived class pointer that is pointing to a derived class object is casted to a base class pointer. This pointer can now access only the base class subobject embedded within the derived class object.

```
PtrCircle = & Ring;
PtrShape = dynamic_cast<Shape *> (PtrCircle);
```

# 11.2.2 Using dynamic_cast to Replace typeid

In some cases, the code using dynamic_cast can be replaced by one using typeid. It is better and is advisable to do so in such cases. The code using typeid checks for the first slot in the virtual table (where the RTTI information is kept). It has the same performance overhead as