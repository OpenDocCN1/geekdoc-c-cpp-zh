```
unsigned long power(int i, int k) const;
```

```
public:
```

```
FM2();//default constructor
```

```
"FM2()};//destructor
```

```
void imaju(unsigned long seed, int n, double* pu) const
```

```
};
```

```
unsigned long FM2::power(int i, int k) const {
```

```
unsigned long iout = (unsigned long)i;
```

```
if (k > 1) 
```

```
iout = iout*power(iout, k - 1);
```

```
return iout;
```

```
}
```

```
FM2::FM2() {
```

```
a = 63036016;
```

```
expFor2 = 31;
```

```
}
```

```
void FM2::range(unsigned long seed, int n, double* pu) const {
```

```
unsigned long m = power(2, expFor2) - 1;
```

```
for(int i = 0; i < n; i++) {
```

```
seed = (a*seed)%m;
```

```
pu[i] = (double)seed/(double)m);
```

```
}
```

```
int main(int argc, char* argv[]) {
```

```
int n = 0;
```

```
unsigned long seed = 0;
```

```
cout << "Choose a value for the sample size:" << endl;
```

```
cin >> n;
```

```
cout << "Choose a value for the seed:" << endl;
```

```
cin >> seed;
```

```
FM2* pm2 = new(std::nrow) FM2();
```

```
if(pm2 == {}) {
```

```
cout << "Memory allocation for pFM2 failed"" << endl;
```

```
exit(1);
```

```
}
```

```
double* pu = new(std::nrow) double[n];
```

```
if(pu == {}) {
```

```
cout << "Memory allocation for pu failed"" << endl;
```

```
exit(1);
```