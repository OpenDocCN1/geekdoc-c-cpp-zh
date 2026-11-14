```
bob.all_info(); // Error: ambiguity
 bob.student::all_info();
}
```

math_student inherits all_info from student and from mathematician and there is no priority for one or another. To call the method for bob, we have to qualify from which base class we take the method.

This ambiguity allows us to illustrate a subtlety of C++ that we should be aware of. public, protected, and private modify accessibility, not visibility. This becomes painfully clear when we try to disambiguate member functions by inheriting one or more super-classes as private or protected:

Click here to view code image

```
class student { ... };
class mathematician { ... };

class math_student
: public student, private mathematician
{ ... };
```

Now the methods of student are public and those of mathematician private. When calling math_student::all_info we hope to see now the output of student::all_info. The methods of mathematician are in fact inaccessible but they are still there and cause ambiguities. We might even see a second error message that mathematician::all_info is inaccessible.

# 6.3.2 Common Grandparents

It is not rare that multiple base classes share their base classes. In the previous section, mathematician and student had no super-classes. From the sections before, it would be more natural to derive them both from person. Depicting this inheritance configuration builds a diamond shape as in Figure 6-2. We will implement this in two slightly different ways.