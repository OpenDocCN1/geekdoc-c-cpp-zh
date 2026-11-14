```
class student
    : public virtual person
{
    protected:
        student(const string& passed) : passed(passed) {}
        void my_info() const { ... }
    ...
};

class mathematician
    : public virtual person
{
    protected:
        mathematician(const string& proved) : proved(proved) {}
        void my_info() const { ... }
    ...
};

class math_student
    : public student, public mathematician
{
    public:
        math_student(const string& name, const string& passed, const string&
            proved) : person(name), student(passed), mathematician(proved) {}
        virtual void all_info() const override {
            student::all_info();
            mathematician::my_info();
        }
    };
};
```