```
void ChangeColor(HTHING hThing, int color) {
 Thing *pThing = NULL;
 if (IsValid(hThing) != false) {
 Thing *pThing = new Thing(hThing);
 pThing->Color(color);
 }

 // Which pThing is this?
 delete pThing;
}
```

In this snippet, two Thing pointers called pThing are declared. The one inside the if statement points to an instance of a Thing object which is never deleted. The pThing that does get deleted is NULL at the time of deletion. C++ guarantees that deleting a null pointer is harmless. Thus, a memory error detection tool may not flag this deletion as an error because it is a valid operation.

A quick glance at the above function makes you think pThing gets deleted, so there seems to be no problem. This is a nice technique to slip past code reviewers.

# Tactic No. 4: Use delete on an Array

To use this tactic, allocate an array with the array new operator (new[]) then release the memory with plain old delete, as in:

```
char *pBuf;
pBuf = new char[100];
delete pBuf; // NOT delete[] pBuf;
```

Probably more than a few readers are suddenly getting a nervous feeling in the pits of their stomachs. If you use the delete operator (and not the delete[] operator) to release an object that was allocated with new[], the resulting behavior is currently undefined. Even if you get away with this operation now it could bite you later. Or, it may simply leak the memory. Go ahead, put some peril in your life and use it liberally.

# Tactic No. 5: Practice Careless Polymorphism

This tactic takes advantage of the fact that destructors are not inherited. In C++, it is possible and in fact highly desirable to store the address of a derived-class object as a pointer to its base class. You get polymorphic behavior by referencing this derived class object through the base class pointer. The following program