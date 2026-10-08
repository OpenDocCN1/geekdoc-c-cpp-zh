```
void user(Vector<int>& vi, list<double>& ld, vector<complex<double>>& vc)
{
    int x = sum(vi,0);                       // the sum of a vector of ints (add ints)
    double d = sum(vi,0.0);                 // the sum of a vector of ints (add doubles)
    double dd = sum(id,0.0);                // the sum of a list of doubles
    auto z = sum(vc,complex{0.0,0.0,0.0});  // the sum of a vector of complex<double>s
}
```