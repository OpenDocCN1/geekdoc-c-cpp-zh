# 684 Introduction to C++

```
class Company
{
private:
    string cmp_name;
    string tax_num;
    int empl;
public:
    Company(const string& cmp_name, const string& tax_num, int empl);
    Company() {cmp_name = "None"; empl = -1;} /* A default
constructor is needed to create the sub-objects of the derived objects. The
exercise does not allow to call the previous constructor. Therefore, in order
to create the base class sub-object contained in the derived object, the
default constructor must be added. **/
    virtual ~Company() {};
    virtual void show() {};
};
```

```
class Software_Cmp : public Company
{
private:
    string prod;
    int prgr;
public:
    Software_Cmp(const string& prod, int prgr);
    virtual void show() const override;
};
```

```
class Finance_Cmp : public Company
{
private:
    string srvc;
    int acnt;
public:
    Finance_Cmp(const string& srvc, int acnt);
    virtual void show() const override;
};
```

```
Company::Cmp(const string& cmp_name, const string& tax_num, int empl)
{
    /* Let's use this pointer to avoid looking for different parameter
   names. */
    this->cmp_name = cmp_name;
    this->tax_num = tax_num;
    this->empl = empl;
}
```

```
void Company::show() const
{
    cout << "N:" << cmp_name << " E:" << empl << '\n';
}
```

```
Software_Cmp::Software_Cmp(const string& prod, int prgr)
{
    this->prod = prod;
    this->prgr = prgr;
}
```