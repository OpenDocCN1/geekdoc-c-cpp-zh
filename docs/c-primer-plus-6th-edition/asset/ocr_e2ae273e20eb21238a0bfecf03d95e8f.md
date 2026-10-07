function so that it can directly access the private data for a class. For example, consider the addition operator for the Time class. It has this prototype in the Time class declaration:

Instead, the class could use the following prototype:

```
// nonmember version
friend Time operator+(const Time & t1, const Time & t2);
```

The addition operator requires two operands. For the member function version, one is passed implicitly via this pointer and the second is passed explicitly as a function argument. For the friend version, both are passed as arguments.

> Note
A nonmember version of overloaded operator function requires as many formal parameters as the operator has. A member version of the same operator requires one fewer parameters because one operand is passed implicitly as the invoking object.

Each of these two prototypes matches the expression T2 + T3, where T2 and T3 are type objects. That, the compiler can convert the statement

```
T1 = T2 + T3;
```

to either of the following:

```
T1 = T2.operator+(T3);      // member function
T1 = operator+(T2, T3);     // nonmember function
```

Keep in mind that you choose one or the other form when defining a given operator, but not both forms match the expression, defining both forms is an ambiguity error, leading to a compilation error.

Which form, is it best to use? For operators, as mentioned earlier, the member function is the only valid choice. Otherwise, it often does not make difference. Sometimes, depending on the class design, the nonmember version may have advantage, particularly if you have defined type conversions for the class.The section "Conversions and Friends," near the end of this chapter, discusses this situation.

# More Overloading: A Vector Class

Let's look at another class design that uses operator overloading and friends—class vertices. This also illustrates further aspects of class design, such as incorporating two ways of describing the same thing into an object. Even if you don't care for vectors, you can use many of the new techniques shown here in other contexts. A vector, as the term is used in engineering and physics, is a quantity that has a magnitude (size) and a direction. For example, if you push something, the effect depends on how hard you push (the magnitude) and in what direction you push. A push in one direction can cause to veer, whereas a push in another direction can hasten its rush to doom. To fully describe the motion of your car, you should give both the speed (the