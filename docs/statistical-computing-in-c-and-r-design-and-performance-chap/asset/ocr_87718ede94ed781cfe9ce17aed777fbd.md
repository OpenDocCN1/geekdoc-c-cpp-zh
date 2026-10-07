```
Matrix matrixObj(2, 3, pMat);
Vector vectorObj(3, pVec);
```

```
pair<Matrix, Vector> pairObj(matrixObj, vectorObj);
tuple<Matrix, pair<Matrix, Vector>, Vector> 
tupleObj1(matrixObj, pairObj, vectorObj);
```

```
get<0>(tupleObj1).printMatrix();
get<1>(tupleObj1).second.printVec();
Matrix newMat(2, 2, 1.
get<0>(tupleObj1) = newMat;
get<0>(tupleObj1).printMatrix();
```

```
tuple<Matrix, pair<Matrix, Vector>, Vector> tupleObj2(tupleObj1);
get<0>(tupleObj2).printMatrix();
```

```
return 0;
```

Objects from three classes are created at the beginning of the program: class Matrix, Vector and pair<Matrix, Vector>. A tuple object is created with slots corresponding to the contents of the first Matrix slot of the pair<Matrix, Vector> object. The get function is used next to print out the contents of the first Matrix slot of the pair<Matrix, Vector> object. It is used again to overwrite the Matrix slot with an identity matrix. a copy of the first tuple object is made and its Matrix slot is printed to standard output. The results from running the program are shown below.

| 1 | 3 | 5 |
| 2 | 5 | 8 |
| 1 | | 0 |
| 0 | | 1 |
| 1 | | 0 |
| 0 | | 1 |