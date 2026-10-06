```
dBest = DBL_MAX;
stStart = { 0 };
stEnd = { 0 };
```

```
for (unsigned uIndex = 0; uIndex < uSize; uIndex++) {
    pdAllele[uIndex] = Random(-65.536, 65.536);
}
dSum += pdAllele[uIndex];

if (dMin > pdAllele[uIndex]) {
    dMin = pdAllele[uIndex];
}
```

```
void CSchwefel::Initialize(unsigned uSize) {
    if (pdAllele == NULL) {
        pdAllele = new double[this->uSize = uSize];
    }
    srand(Seed());
```

```
dSum = 0;
dMin = DBL_MAX;
dScore = 0;
dBest = DBL_MAX;
stStart = { 0 };
stEnd = { 0 };
```

```
for (unsigned uIndex = 0; uIndex < uSize; uIndex++) {
    pdAllele[uIndex] = Random(-65.536, 65.536);
}
dSum += pdAllele[uIndex];

if (dMin > pdAllele[uIndex]) {
    dMin = pdAllele[uIndex];
}
```