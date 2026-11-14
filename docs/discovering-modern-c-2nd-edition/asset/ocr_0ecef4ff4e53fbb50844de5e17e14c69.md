```
class student
: public person
{
public:
student(const string& name, const string& passed)
: person(name), passed(passed) {}
void all_info() const {
cout << "[student] My name is " << get_name() << endl;
cout << "I passed the following grades: " << passed << endl;
}
private:
string passed;
};
```