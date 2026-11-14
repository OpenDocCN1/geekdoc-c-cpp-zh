```
int ai[] = {2, 4, 7};
double ad[] = {2., 4.5, 7.};
cout << "sum ai is " << accumulate_array(ai, &ai[3]) << '\n';
cout << "sum ad is " << accumulate_array(ad, ad+3) << '\n';
```