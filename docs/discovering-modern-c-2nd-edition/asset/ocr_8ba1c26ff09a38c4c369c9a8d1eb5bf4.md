```
struct identity_test
{
    template <typename T>
    static void eval()
    {
        T zero[0], one[1], nine[9];
        if (zero + nine != nine)
            throw logic_error("Addition wrong");
        if (one * nine != nine)
            throw logic_error("Multiplication wrong");
        cout << "Test passed for " << typeid(T).name() << endl;
    }
};
```