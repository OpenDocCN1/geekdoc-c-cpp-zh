# 17.4. POLYMORPHISM

```
connector (conn) {
    string get() const override {
        return left_bracket + Text::get() + right_bracket;
    }
};
// The text is always the word FIXED
class FixedText : public Text {
public:
    FixedText() : Text("FIXED") {}
};
int main() {
    vector<Text*> texts = { new Text("Wow"),
                               new FancyText("Wee", " ":", "[", ":-"),
                               new FixedText,
                               new FancyText("Whoa", " ":", ":", ":") };
    for (auto t : texts) {
        cout << t->get() << endl;
    }
}
```

We know from Section 11.1 that a vector is a collection of homogeneous elements. Homogeneity means the elements in a vector must be of the same type. Homogeneity takes a deeper meaning when inheritance is a relationship involved. Listing 17.4 (polymorphicvector.cpp) the declared type of the texts **vector<Text*>**. With inheritance, only texts hold pointers to simple objects, it simultaneously can hold pointers to FixedText and FancyText objects. Listing 17.4 (polymorphicvector.cpp) prints

![](bbox=[0.118, 0.532, 0.792, 0.638])

As we can see, the expression t->get() in the main function is polymorphic; the actual get method invoked—Text::FancyText::get or FixedText::get—depends on the exact type of t. As t assumes the value of each element in the vector's loop, the exact type of t points to varies. Even though all elements of the texts are pointers to objects, only one of the elements points to a pure text; the rest of the elements are FancyText or FixedText objects.

Why we use pointers rather than the objects they achieve to achieve polymorphism? Because pointer stores a memory address (see Section 10.6). Points, no matter what type they point to, are all the same size (4 bytes on 32-bit systems and 6 bytes on 64-bit systems). Text objects and FancyText objects are not larger than the same size (see Figure 17.1 for a conceptual picture); FancyText objects are bigger, containing extra string fields. All the elements of a vector must be the same size. If we use a vector of Text objects, when we assign FancyText object to an element in the texts the assignment would slice the extra fields in the FancyText object. Pointer assignment avoids the slicing problem.

The main reason for using pointers in C++ is static binding for all methods (virtual and non-virtual) invoked on behalf of an object; the compiler chooses the method based on the declared type of

©2014 Richard L. Halterman

Draft date: January 26, 2014