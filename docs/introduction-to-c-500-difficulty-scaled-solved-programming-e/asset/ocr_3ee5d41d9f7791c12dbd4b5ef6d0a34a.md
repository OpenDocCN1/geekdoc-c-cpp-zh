```
class Person
private:
  string name;
  int code;
public:
  Person() {name = "None"; code = 0};
  Person(const string& n, int c) : name(n), code(c) {}
  virtual ~Person() {}
  virtual void show() const;
};

void Person::show() const
{
  cout << "\nName:" << name << ' ' << "Code:" << code << ' '';
}
```

```
class Programmer : public Person
private:
  string cmp; // The number of the company (s)he is working at.
public:
  Programmer() {cmp = "Any";}
  Programmer(const string& n, int c, const string& s) : Person(n, c), cmp(s) {}
  virtual void show() override;
};

void Programmer::show() const
{
  Person::show();
  cout << "Company:" << cmp;
}
```

```
class Author : public Person
private:
  int titles; // The number of the books (s)he has written.
public:
  Author() {titles = 0};
  Author(const string& n, int c, int t) : Person(n, c), titles(t) {}
  virtual void show() override;
};

void Author::show() const
{
  Person::show();
  cout << "Titles:" << titles;
}
```

```
class ProgAuth : public Programmer, public Author

```