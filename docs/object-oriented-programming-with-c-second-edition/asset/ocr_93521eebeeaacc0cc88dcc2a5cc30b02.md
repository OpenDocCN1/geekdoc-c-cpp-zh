```
public:
void setFeet(int x) {
    iFeet=x;
}
int getFeet() {
    return iFeet;
}
void setInches(float y) {
    fInches=y;
}
float getInches() {
    return fInches;
}
```

can also be written as

```
struct Distance {
    void setFeet(int x) //public by default
    iFeet=x;
    int getFeet() //public by default
    return iFeet;
    void setInches(float y) //public by default
    fInches=y;
    float getInches() //public by default
    return fInches;
}private:
    int iFeet;
    float finches;
```

Listing 2.4, the member functions have not been placed under any access modifier. Therefore, there are public members by default.
On the other hand, class members are private by default. This is the only difference between the class keyword and the struct keyword.
Thus, the structure Distance can be redefined by using the class keyword as shown in Listing 2.5.

+   Listing 2.5 Class members are private by default

```
class Distance {
    int iFeet; //private by default
    float finches; //private by default
```