# NONUNIFORM GENERATION

```
double Finv(double u, double lambda){
  return (-log(1 - u)/lambda);
}
```

```
int main(int argc, char* argv[]){
  double lambda; int n;

  cout << "Input the value for lambda:" << endl;
  cin >> lambda;

  unsigned long seed1, seed2, seed3;
  cout << "Choose a value for the sample size:" << endl;
  cin >> n;
  cout << "Choose a value for seed1:" << endl;
  cin >> seed1;
  cout << "Choose a value for seed2:" << endl;
  cin >> seed2;
  cout << "Choose a value for seed3:" << endl;
  cin >> seed3;

  WH* pwh = new(std::nrow) WH();
  if(pwh == 0){
    cout << "Memory allocation for WH failed" << endl;
    exit(1);
  }

  double* pu = new(std::nrow) double[n];
  if(pu == 0){
    cout << "Memory allocation for double pointer failed" << endl;
    exit(1);
  }

  pwh->range(seed1, seed2, seed3, n, pu);
  cout << "Your random numbers are " << endl;
  for(int i = 0; i < n; i++) {
    cout << Finv(pu[i], lambda) << " ";
  }
  cout << endl;
  delete pWH;
  delete []pu;
  return 0;
}
```

The only new aspect in List 4.7 is the specification of the $F^{-1}$ function at the beginning of the program and its use in the for loop to transform the uniform numbers obtained from the WH pointer pWH. It is also necessary to include the cmath header in order to use the natural logarithm function log in our Finv function. Upon compilation to the executable driverExp, the program produces output as

```
./driverExp
Input the value for lambda:
1
Choose a value for the sample size:
5
Choose a value for seed1:
123
Choose a value for seed2:
456
Choose a value for seed3:
```