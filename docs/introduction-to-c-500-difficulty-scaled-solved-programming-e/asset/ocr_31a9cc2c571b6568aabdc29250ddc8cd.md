# 20 • Inheritance 665

Thus, if we change Circle to:

```
class Circle : public Shape
{
public:
    virtual void draw() override {std::cout << "Circle ";n    Shape sh;
};
```

and write: cir.sh.draw();
which draw(1) will be called? That of Circle or Shape? I won't tell you the answer, find it by yourself.

As we said, if a function of the base class may be overridden in derived class, we declare it virtual. Otherwise, do not make it virtual, not only to avoid some extra memory and the overhead to process its call, as we saw earlier with the vtable, but also to make it to someone who reads the class design that it is not our intention to be overridden.

Let's look at another example of the uselessness of virtual functions. Suppose we want to manage a collection of Product and Book objects. We cannot use an ordinary array or vector variable to store the objects, because the type of elements must be the same. However, we can use an array of pointers to Product objects. And by a pointer to a Product object can also point to an object of the derived Book class, we can use this array and apply virtual functions to manage both of objects as we wish. In the general case, thanks to the virtual functions we can use a single array of pointers to manage different types of objects. Let's see the program:

```
int main() // Example 20.12
{
    const int SIZE = 10;

    int i, ch;
    float prc;
    string code, title, auth;
    Product *p[SIZE];

    for(i = 0; i < SIZE; i++)
    {
        cout << "Enter choice (1 for Product): ";
        cin >> ch;

        cout << "Enter code: ";
        cin >> code;
        cout << "Enter price: ";
        cin >> prc;
        if(ch == 1)
            p[i] = new Product(code, prc);
        else
        {
            cout << "Enter title: ";
            cin >> title;
            cout << "Enter auth: ";
            cin >> auth;
            p[i] = new Book(code, prc, title, auth);
        }
    }
}
```