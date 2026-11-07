```
```cpp
        void ShowObject() const;
    public:
        Useless();
        explicit Useless(int k);
        Useless(int k, char ch);
        Useless(const Useless & f);     // regular copy constructor
        Useless(Useless && f);          // move constructor
        ~Useless();
        Useless operator+(const Useless & f)const;
    // need operator= in copy and move versions
        void ShowData() const;
    };


    // implementation
    int Useless::ct = 0;

    Useless::Useless()
    {
        ++ct;
        n = 0;
        pc = nullptr;
        cout << "default constructor called; number of objects: " << ct << endl;
        ShowObject();
    }

    Useless::Useless(int k) : n(k)
    {
        ++ct;
        cout << "int constructor called; number of objects: " << ct << endl;
        pc = new char[n];
        ShowObject();
    }

    Useless::Useless(int k, char ch) : n(k)
    {
        ++ct;
        cout << "int, char constructor called; number of objects: " << ct
             << endl;
        pc = new char[n];
        for (int i = 0; i < n; i++)
            pc[i] = ch;
        ShowObject();
    }

    Useless::Useless(const Useless & f) : n(f.n)
    {
```
```