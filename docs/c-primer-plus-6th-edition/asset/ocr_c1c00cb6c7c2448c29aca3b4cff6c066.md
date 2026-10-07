```
// const double (**pb)(const double *, int) = pa;
cout << "\nUsing an array of pointers to functions:\n";
cout << "  Address Value\n";
for (int i = 0; i < 3; i++) {
    cout << pa[i](av,3) << " : " << *pa[i](av,3) << endl;
}
cout << "\nUsing a pointer to a function:\n";
cout << "  Address Value\n";
for (int i = 0; i < 3; i++) {
    cout << pb[i](av,3) << " : " << *pb[i](av,3) << endl;
}

// about how a pointer to an array of function pointers
cout << "\nUsing pointers to an array of pointers:\n";
cout << "  Address Value\n";
// easy way to declare pc
auto pc = &pa;
// pre-C11 can use the following code instead
const double (*(*pc)[3])(const double *, int) = &pa;
cout << *(*pc)[0](av,3) << " : " << *(*pc)[0](av,3) << endl;
// hard way to declare pd
const double (*(*pd)[3])(const double *, int) = &pd;
// store return value in pd
const double pdb = (*pd)[1](av,3);
cout << *pdb << " : " << *pdb << endl;
// alternative notation
cout << *(*pd)[2])(av,3) << " : " << *(*pd)[2])(av,3) << endl;
cin.get();
return 0;
}

// some other dull functions
const double * f1(const double * ar, int n) {
    return ar;
}
const double * f2(const double ar[], int n) {
    return ar+1;
}
const double * f3(const double *ar, int n) {
    return ar+2;
}
```