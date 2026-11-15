```
AjPShort2d shorts = NULL;
shorts = ajShort2dNew();
/* The objects are instantiated and ready for use */
```

# 6.17.8.2 Default object destruction

You must free the memory for an object once your are finished with it. The default destructor functions have the suffix Del and take the address of the appropriate object as an argument:

```
void ajCharrDel (AjPChar* Parr);
void ajShortDel (AjPShort* Parr);
void ajShort2dDel (AjPShort2d* Parr);
void ajShort3dDel (AjPShort3d* Parr);
void ajUintDel (AjPUint* Parr);
void ajUint2dDel (AjPUint2d* Parr);
void ajUint3dDel (AjPUint3d* Parr);
void ajIntDel (AjPInt* Parr);
void ajInt2dDel (AjPInt2d* Parr);
void ajInt3dDel (AjPInt3d* Parr);
void ajFloatDel (AjPFloat* Parr);
void ajFloat2dDel (AjPFloat2d* Parr);
void ajFloat3dDel (AjPFloat3d* Parr);
void ajLongDel (AjPLong* Parr);
void ajLong2dDel (AjPLong2d* Parr);
void ajLong3dDel (AjPLong3d* Parr);
void ajDoubleDel (AjPDouble* Parr);
void ajDouble2dDel (AjPDouble2d* Parr);
void ajDouble3dDel (AjPDouble3d* Parr);
```

For example to free memory allocated by array input from the ACD file use:

```
void ajFloatDel (AjPFloat* Parr);
```

It is used as follows:

```
AjPFloat thresholds=NULL;
thresholds = ajAcdGetArray("thresholds");
/* Do something with the array */
ajFloatDel(&thresholds);
```

It is the responsibility of the calling function to destroy any objects once they are finished with:

```
AjPShort2d shorts = NULL;
shorts = ajShort2dNew();
/* The object is instantiated and ready for use */
/* Do something with the instantiated objects */
ajShort2dDel(&shorts);
/* The memory is freed and the pointers reset to NULL, ready for re-use. */
shorts = ajShort2dNew();
/* Do something else with the new objects. The pointer variable is reallocated. */
```