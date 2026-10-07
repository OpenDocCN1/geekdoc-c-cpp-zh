
# 第17章 离散隐尔马尔可夫模型

```cpp
// DNAMark.cpp

#include <iostream>
#include <fstream>
#include <sstream>
#include <string>
using namespace std;

int main(void)
{
    ifstream in("DNA.txt");
    stringstream buffer;
    buffer << in.rdbuf();
    string seq = buffer.str();
    int length = seq.length();
    cout << length << endl;
    cout << seq << endl;
}
```

```cpp
int AA, AC, AG, AT, CA, CC, CG, CT, GA, GC, GG, GT, TA, TC, TG, TT;
AA = AC = AG = AT = 0; CA = CC = CG = 0;
GA = GC = GG = GT = 0; TA = TC = TG = TT = 0;
int sumA, sumC, sumG, sumT; sumA = sumC = sumG = sumT = 0;
```

## 17.5 隐藏马尔可夫模型的应用

```cpp
for(int i=0; i<length-1; i++) {
    if(seq[i]=='A' && seq[i+1]=='A') AA++;
    if(seq[i]=='A' && seq[i+1]=='C') AC++;
    if(seq[i]=='A' && seq[i+1]=='G') AG++;
    if(seq[i]=='A' && seq[i+1]=='T') AT++;
    if(seq[i]=='C' && seq[i+1]=='A') CA++;
    if(seq[i]=='C' && seq[i+1]=='C') CC++;
    if(seq[i]=='C' && seq[i+1]=='G') CG++;
    if(seq[i]=='C' && seq[i+1]=='T') CT++;
    if(seq[i]=='G' && seq[i+1]=='A') GA++;
    if(seq[i]=='G' && seq[i+1]=='C') GC++;
    if(seq[i]=='G' && seq[i+1]=='G') GG++;
    if(seq[i]=='G' && seq[i+1]=='T') GT++;
    if(seq[i]=='T' && seq[i+1]=='A') TA++;
    if(seq[i]=='T' && seq[i+1]=='C') TC++;
    if(seq[i]=='T' && seq[i+1]=='G') TG++;
    if(seq[i]=='T' && seq[i+1]=='T') TT++;
}
```

```cpp
cout << AA << endl; cout << AC << endl;
cout << AG << endl; cout << AT << endl;
cout << CA << endl; cout << CC << endl;
cout << CG << endl; cout << CT << endl;
cout << GA << endl; cout << GC << endl;
cout << GG << endl; cout << GT << endl;
cout << TA << endl; cout << TC << endl;
cout << TG << endl; cout << TT << endl;
```

```cpp
int sum = AA + AC + AG + AT + CA + CC + CG + CT +
          GA + GC + GG + GT + TA + TC + TG + TT;
cout << sum << endl;
sumA = (double)AA + (double)AC + (double)AG + (double)AT; 
sumC = (double)CA + (double)CC + (double)CG + (double)CT;
sumG = (double)GA + (double)GC + (double)GG + (double)GT; 
sumT = (double)TA + (double)TC + (double)TG + (double)TT;
```

```cpp
string out;
double P = 0.0;
out = s;
int T1 = out.length();
double* previous_alpha = new double[N+1];
double* current_alpha = new double[N+1];
// 初始化
for(int i=1;i<=N;i++) previous_alpha[i] = pi(i)*b(i,1,out);
// 归纳
for(int t=1;t<T1; t++) {
  for(int j=1;j<=N; j++) { double sum = 0.0;
  for(int i=1;i<=N; i++) { sum += previous_alpha[i]*a(i,j);
  current_alpha[j] = sum*b(j,t+1,out);
  }
  for(int c=1;c<=N;c++) previous_alpha[c] = current_alpha[c];
}
// 终止
for(int i=1;i<=N;i++) P += previous_alpha[i];
delete[] current_alpha; delete[] previous_alpha;
return P;
```

```cpp
double HMM::beta(const string s)
{
double P = 0.0;
s = s;
int T = o.length();
double* next_beta = new double[N+1];
double* current_beta = new double[N+1];
// 初始化
for(int i=1;i<=N;i++) next_beta[i] = 1.0;
// 归纳
double sum;
for(int t=T-1;t>=1; t--) {
  for(int i=1;i<=N; i++) { sum = 0.0;
  for(int j=1;j<=N; j++) { sum += a(i,j)*b(j,t+1)*next_beta[j];
  current_beta[i] = sum;
  }
  for(int c=1;c<=N;c++) next_beta[c] = current_beta[c];
}
// 终止
for(int i=1;i<=N;i++) P += next_beta[i]*pi(i)*b(i,1);
delete[] next_beta; delete[] current_beta;
return P;
}
```

```cpp
double HMM::gamma(int t, int i)
{ return alpha_table[t][i]*beta_table[t][i]/(alpha_beta_table[t]); }
```

## 17.6. C++ 程序

```cpp
int HMM::index(const char c) {
switch(c) { case 'H': return 0; case 'T': return 1;
default: error("no legal input symbol!");
return 0;
}
}
```

```cpp
double HMM::viterbi(const string s,int best_path[])
{
double P_star = 0.0;
string o = s;
int T = o.length();
double* previous_delta = new double[N+1];
double* current_delta = new double[N+1];
int** psi = new int[T+1];
for(int i=0;i<T;i++) psi[i] = new int[N+1];
// 初始化
for(int i=1;i<N;i++) {
previous_delta[i] = pi(i)*b(i,1); psi[1][i] = 0; }
double tmp, max;
// 递归
for(int t=2;t<T;t++) {
  for(int j=1;j<N;j++) { max = 0.0;
  for(int i=1;i<N;i++) { tmp = previous_delta[i]*a(i,j);
if(tmp >= max) { max = tmp; psi[t][j] = i; }
}
current_delta[j] = max*b(j,t);
}
for(int c=1;c<N;c++) previous_delta[c] = current_delta[c];
} // 终止
for(int i=1;i<N;i++) {
if(previous_delta[i] >= P_star) {
P_star = previous_delta[i]; best_path[T] = i;
}
} // 获取序列;
for(int t=T-1;t>=1;t--) best_path[t] = psi[t][best_path[t]];
best_path[T] = -1;
for(int i=0;i<T;i++) delete psi[i];
delete[] psi; delete[] previous_delta; delete[] current_delta;
return P_star;
}
```

```cpp
double** HMM::construct_alpha_table()
{
double** alpha_table = new double*[T+1];
for(int i=0;i<=T+1;i++) alpha_table[i] = new double[N+1];
// 初始化
for(int i=1;i<N;i++) alpha_table[1] [i] = pi(i)*b(i,1);
// 归纳
for(int t=1;t<T;t++) {
for(int j=1;j<=N;j++) { double sum = 0.0;
for(int i=1;i<=N;i++) { sum += alpha_table[t][i]*a(i,j); }
alpha_table[t+1][j] = sum*b(j,t+1);
}
return alpha_table;
}
```

```cpp
double** HMM::construct_beta_table()
{
double** beta_table = new double[T+1];
for(int i=0;i<=T+1;i++) beta_table[i] = new double[N+1];
// 初始化
for(int i=1;i<N;i++) beta_table[T][i] = 1.0;
// 归纳
double sum;
for(int t=T-1;t>=1; t--) {
for(int i=1;i<=N;i++) { sum = 0.0;
for(int j=1;j<=N; j++) { sum += a(i,j)*b(j,t+1)*beta_table[t+1]; }
beta_table[t][i] = sum;
}
return beta_table;
}
```

```cpp
double* HMM::construct_alpha_beta_table()
{
double* alpha_beta_table = new double[T+1];
for(int t=1;t<T;t++) alpha_beta_table[t] = 0;
for(int i=1;i<N;i++) {
// 注意：原始 OCR 源中的逻辑不完整，
// 但保持提供的文本结构。
}
return alpha_beta_table;
}
```

```cpp
double* HMM::construct_xi_divisor()
{
double* xi_divisor = new double[T+1];
double sum_j;
for(int t=1;t<T;t++) { xi_divisor[t] = 0.0;
for(int i=1;i<N;i++) { sum_j = 0.0;
for(int j=1;j<=N;j++) {
    sum_j += alpha_table[t][i]*a(i,j)*beta_table[t+1][j];
}
xi_divisor[t] += sum_j;
}
}
return xi_divisor;
}
```

```cpp
double HMM::xi(int t, int i, int j)
{
    return ((alpha_table[t][i]*a(i,j)*b(j,t+1)*beta_table[t+1][j])/xi_divisor[t]);
}
```

```cpp
void HMM::reestimate_pi()
{
    for(int i=1;i<N;i++) {
        reestimated->set_pi(i,gamma(1,i));
    }
}
```

```cpp
void HMM::reestimate_a()
{
    double sum_xi, sum_gamma;
    for(int i=1;i<N;i++) {
        for(int j=1;j<=N;j++) { sum_xi = 0.0, sum_gamma = 0.0;
        for(int t=1;t<T;t++) { sum_xi += xi(t,i,j); sum_gamma += gamma(t,i); }
        reestimated->set_transition(i,j,sum_xi/sum_gamma);
    }
}
```

```cpp
void HMM::reestimate_b()
{
    double sum_gamma, tmp_gamma;
    double sum_gamma_output;
    for(int j=1;j<=N;j++) {
        for(int k=0;k<M;k++) { sum_gamma = 0.0, sum_gamma_output = 0.0;
        for(int t=1;t<T;t++) { tmp_gamma = gamma(t,j);
        if(index(o[t-1])==k) { sum_gamma_output += tmp_gamma; }
        sum_gamma += tmp_gamma;
    }
        reestimated->set_emission(j,k,sum_gamma_output/sum_gamma);
    }
}
```

# 第17章 离散隐尔马尔可夫模型

```cpp
void HMM::forward_backward(string o)
{
    T = o.length();
    alpha_table = construct_alpha_table();
    beta_table = construct_beta_table();
    alpha_beta_table = construct_alpha_beta_table();
    xi_divisor = construct_xi_divisor();
    reestimate(pi); reestimate(a); reestimate(b);
    for(int t=1; t<T; t++) delete alpha_table[t];
    delete [] alpha_table;
    for(int t=1; t<T; t++) delete beta_table[t];
    delete[] beta_table; delete[] alpha_beta_table; delete[] xi_divisor;
    Data* temp_value = current;
    current = reestimated;
    reestimated = temp_value;
}
```

```cpp
void HMM::maximize(string o, string test)
{
    double diff_entropy, old_cross_entropy, new_cross_entropy;
    int c = 1;
    int t = test.length();
    old_cross_entropy = -log10(P);
    cout << "Initial entropy: " << old_cross_entropy << "\n";
    do {
        forward_backward(o);
        new_cross_entropy = -log10(P);
        diff_entropy = old_cross_entropy - new_cross_entropy;
```

