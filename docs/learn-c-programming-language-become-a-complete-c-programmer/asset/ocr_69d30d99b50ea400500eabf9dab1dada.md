argument or a nonmember function taking two arguments. For any binary operator @, aa@bb can be interpreted as either aa.operator@(bb) or operator@(aa,bb). If both are defined, overload resolution (§12.3) determines which, if any, interpretation is used. For example:

```
class X {
public:
void operator+(int);
X(int);
};

void operator+(X,X);
void operator+(X,double);

void f(X a) {
a+1; // a.operator+(1)
1+a; // ::operator+(X(1),a)
a+1.0; // ::operator+(a,1.0)
}
```

A unary operator, whether prefix or postfix, can be defined by either a nonstatic member function taking no arguments or a nonmember function taking one argument. For any prefix unary operator @, @aa can be interpreted as either aa.operator@() or operator@(aa). If both are defined, overload resolution (§12.3) determines which, if any, interpretation is used. For any postfix unary operator @, aa@ can be interpreted as either aa.operator@(int) or operator@(aa,int). This is explained further in §19.2.4. If both are defined, overload resolution (§12.3) determines which, if any, interpretation is used. An operator can be declared only for the syntax defined for it in the grammar (§iso.A). For example, a user cannot define a unary % or a ternary +. Consider:

```
class X {
public: // members (with implicit this pointer):
X *operator&(); // prefix unary&(address of) X operator&(X); // binary & (and)
X operator++(int); // postfix increment (see §19.2.4) X operator&(X,X); // X
operator/(); //
};
error : ternary error : unary /
```

# Section 18.2.1 Binary and Unary Operators 531

```
// nonmember functions :
X operator -(X); // prefix unaryminus X operator-(X,X); // binary minus X operator--(X&,int); // postfix decrement X operator-(); // X operator-(X,X,X); // X operator%(X); //
error : no oper and error : ternary
error : unary %
```

Operator [] is described in §19.2.1, operator () in §19.2.2, operator-> in §19.2.3, operators