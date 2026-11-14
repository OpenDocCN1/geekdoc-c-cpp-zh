```
class complex
{
public:
    double get_r() { return r; }       // Causes clumsy
    void set_r(double newr) { r = newr; } // code
    double get_i() { return i; }
    void set_i(double newi) { i = newi; }
private:
    double r, i;
};
```