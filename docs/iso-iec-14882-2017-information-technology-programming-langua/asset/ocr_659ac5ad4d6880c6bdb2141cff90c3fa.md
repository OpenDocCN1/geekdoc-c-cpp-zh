# ISO/IEC 14882:2017(E)

```
friend void c0(); // error
};
X* px; // OK, but :X is found
nZ* pz; // error, no Z is found
```

// end example

# 14.4 Protected member access

An access check beyond those described earlier in Clause 14 is applied when a non-static member or non-static function is a member of its naming class (14.2).¹¹⁵ As described earlier, access to a protected member is granted because the reference occurs in a friend or member of some class C. If the access is to form a pointer to member (8.3.1), the nested-name-specifier shall denote C or a class derived from C. All other accesses allow a (possibly implicit) object expression (8.2.5). In this case, the class of the object shall be C or a class derived from C. | Example:

```
class B {
protected:
int i;
static int j;
};
class D1 : public B {
friend void fr(B*, D1*);
};
class D2 : public B {
friend void fr(B*, D1*, D2*);
void mem(B*);
};
void fr(B* pb, int* p1, D2* p2) {
pb->i = 1; // ill-formed
p1->i = 2; // OK (access through a D2)
p2->i = 4; // OK (access through a D2, even though naming class is B)
int B::pmi_B = &B::i; // OK
int B::pmi_B2 = &D2::i; // OK (type of D2::i is int B::)
B::j = 5; // ill-formed (not a friend of naming class B)
D2::j = 6; // OK (refers to static member)
}
g(B* pb, int p1, int p2) {
pb->i = 1; // ill-formed
```

¹¹⁵ This additional check does not apply to other members, e.g., static data members or enumerator member constants.