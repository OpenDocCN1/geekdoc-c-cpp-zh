```
class person
{
public:
    person() {}
    explicit person(const string& name) : name(name) {}

    void set_name(const string& n) { name= n; }
    string get_name() const { return name; }
    void all_info() const
    { cout << "[person] My name is " << name << endl; }

private:
    string name;
};
```