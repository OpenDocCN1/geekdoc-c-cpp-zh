# GENERATION OF PSEUDO-RANDOM NUMBERS

```
return val;
}
```

```
void binMult(bool** pb, int p, int q, int r){
//use the extra row of pb here
for(int j = 0; j < r; j++){
    pb[p][j] = pb[0][j]*pb[q][j];
}
//Update pb
for(int i = 0; i < p; i++) {
    for(int j = 0; j < r; j++) {
        pb[i][j] = pb[i + 1][j];
    }
}
```

```
int main(){
    int r;
    std::cout << "Input the value for r:" << std::endl;
    std::cin >> r;
    int p;
    std::cout << "Input the value for p:" << std::endl;
    std::cin >> p;
    int q;
    std::cout << "Input the value for q:" << std::endl;
    std::cin >> q;
    unsigned long* x0 = new unsigned long[p];
    std::cout << "Input a " << p << " integer seed:" << std::endl;
    for(int i = 0; i < p; i++) {
        std::cin >> x0[i];
    }
```

```
unsigned long modulus = power(2, p) - 1;
//matrix of Booleans to hold the bits
bool** pb = new bool*[p + 1];
//rows will hold the integer bit-wise representations
//extra row added for temporary storage
for(int i = 0; i < (p + 1); i++) {
    pb[i] = new bool[r];
```

```
//initialize the bit pattern using x0
for(int i = 0; i < p; i++)
    intToBin(x0[i], pb[i], r);
```

```
//generate the "data"
for(int i = 0; i < (modulus - p); i++){
    binMult(pb, p, q, r);
    std::cout << " " << binToInt(pb[p - 1], r) << " ";
}
std::cout << std::endl;
nreturn 0;
}
```

In the beginning of segment Listing 4.3 the user is queried for values of the parameters, p, q and the number of bits r that are to be used in constructing the generated integers. The p integers that will provide the seed for the generator are also required as user input. In