# Object-Oriented Programming with C++

```
APtr->x=10;      //line 5. OK. Can access public
//member of the base class through a base
//class pointer.

}/*End of protectedInheritance.cpp*/
```

A base class pointer cannot point to an object of a derived class that has been derived by using the private access specifier. Let redefine the xyz() function from the program (Listing 5.23) as in Listing 5.24 and see what happens if we recompile the program.

**Listing 5.24** A base class pointer cannot point at an object of the private-derived class

```
/*Beginning of privateInheritance.cpp*/
class A
{
private:
int x;
protected:
int y;
public:
int z;
};
class B : private A      //B is a private derived class of A
{
public:
void f1(){
nx=1;      //ERROR: private member remains private
y=2;      //OK: protected member becomes private in
//this class
z=2;      //OK: protected member becomes private in
//this class
}
class C : public B
{
public:
void f2(){
x=1;      //ERROR: private member remains private
y=2;      //ERROR: private member remains private
z=2;      //ERROR: private member remains private
}
void xyz(B* Bptr) //non-member function
Bptr->x=10;      //ERROR: private member remains private
Bptr->y=20;      //ERROR: protected member becomes private
Bptr->z=30;      //ERROR: public member becomes private
}
/*End of privateInheritance.cpp*/
```

Line 4 of Listing 5.24 will not compile because line 2 and 5 will compile. Line 2 will not compile although 'z' is a public member of the base class A, B is derived from class A by using the private access specifier. In this case, the base pointer might access the object of a private-derived class in a way (line 5 of Listing 5.24)