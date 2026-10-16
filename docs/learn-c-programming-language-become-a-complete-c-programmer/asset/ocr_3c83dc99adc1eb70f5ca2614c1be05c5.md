The **dynamic_cast** operator takes two operands: a type bracketed by `<` and `>`, and a pointer or reference bracketed by `(` and `)`. Consider first the pointer case:

```
dynamic_cast<T*>(p)
```

If p is of type T* or of a type D* where T is a base class of D, the result is exactly as if we had simply assigned p to a T*. For example:

```
class BB_ival_slider : public Ival_slider, protected BBslider {
// ...
};

void f(BB_ival_slider * p) {
Ival_slider* pi1 = p; // OK Ival_slider* pi2 = dynamic_cast<Ival_slider*>(p); // OK

BBslider* pbb1 = p; // error : BBslider is a protected base BBslider* pbb2 =
dynamic_cast<BBslider*>(p); // OK: pbb2 becomes nullptr
}
```

This (the upcast) is the uninteresting case. However, it is reassuring to know that **dynamic_cast** doesn’t allow accidental violation of the protection of private and protected base classes. Since a **dynamic_cast** used as an upcast is *exactly* like a simple assignment, it implies no overhead and is sensitive to its lexical context.

The purpose of **dynamic_cast** is to deal with the case in which the correctness of the conversion cannot be determined by the compiler. In that case, **dynamic_cast<T*>(p)** looks at the object pointed to by **p** (if any). If that object is of class **T** or has a unique base class of type **T**, then **dynamic_cast** returns a pointer of type **T*** to that object; otherwise, **nullptr** is returned. If the value of **p** is **nullptr**, **dynamic_cast<T*>(p)** returns **nullptr**. Note the requirement that the conversion must be to a uniquely identified object. It is possible to construct examples where the conversion fails and **nullptr** is returned because the object pointed to by **p** has more than one subobject representing bases of type **T** (§22.2).

A **dynamic_cast** requires a pointer or a reference to a polymorphic type in order to do a downcast or a crosscast. For example:

```
class My_slider: public Ival_slider { // polymorph pibcase (Ival_slider has virtual
functions) // ...
};

class My_date : public Date { // base not polymorphic (Date has no virtual functions) //
...
};

void g(Ival_box * pb, Date* pd) {
My_slider* pd1 = dynamic_cast<My_slider*>(pb); // OK
My_date* pd2 = dynamic_cast<My_date*>(pd); // error : Date not polymorphic
}
```

Requiring the pointer’s type to be polymorphic simplifies the implementation of **dynamic_cast** because it makes it easy to find a place to hold the necessary information about the object’s type. A typical implementation will attach a “type information object”