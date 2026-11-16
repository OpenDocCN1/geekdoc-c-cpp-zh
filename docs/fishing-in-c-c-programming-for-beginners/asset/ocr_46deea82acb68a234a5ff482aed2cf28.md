```
~Counter(){}
USHORT GetItsVal()const { return itsVal; }
void SetItsVal(USHORT x) {itsVal = x; }
Counter operator+ (const Counter &);

private:
    USHORT itsVal;
};

Counter::Counter(USHORT initialValue):
    itsVal(initialValue)
{}

Counter::Counter():
    itsVal(0)
{}

Counter Counter::operator+ (const Counter & rhs)
{
    return Counter(itsVal + rhs.GetItsVal());
}

int main()
{
    Counter first(2), second(4), third;

    third = first + second;

    cout << "first: " << first.GetItsVal()<< endl;
```