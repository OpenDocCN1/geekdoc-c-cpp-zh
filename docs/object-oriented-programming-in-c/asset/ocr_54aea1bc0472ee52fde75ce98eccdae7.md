```
class invent2      // destination class
{
    int code;
    float value;
    public:
    invent2()
    {
        code = 0; value = 0;
    }
    invent2(int x, float y)      // constructor for
                                 // initialization
    {
        code = x;
        value = y;
    }
    void putdata()
    {
        cout << "Code:  " << code << "\n";
        cout << "Value: " << value << "\n\n";
    }
    invent2(invent1 p)           // constructor for conversion
    {
        code = p.getcode();
        value = p.getitems() * p.getprice();
    }
};  // End of destination class

int main()
{
    invent1 s1(100,5,140.0);
    invent2 d1;
    float total_value;

    /* invent1 To float */
    total_value = s1;

    /* invent1 To invent2 */
    d1 = s1;

    cout << "Product details - invent1 type" << "\n";
    s1.putdata();

    cout << "\nStock value" << "\n";
    cout << "Value = " << total_value << "\n\n";

    cout << "Product details-invent2 type" << "\n";
    d1.putdata();
    return 0;
}
```