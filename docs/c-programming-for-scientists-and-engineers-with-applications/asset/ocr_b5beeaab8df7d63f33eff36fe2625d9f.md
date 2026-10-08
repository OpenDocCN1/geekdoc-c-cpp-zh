```
funcsumdepth: (file1)
sumdepth ← sumdepth + depth
return sumdepth
```

```
funcsumpressress(file1)
sumpressure ← suppressure + pressure
return suppressure
```

```
funcinput: (file2)
input depth
```

```
funcpressure: (file3)
pressure ← .4333333 × depth
return
```

```
funcoutput: (file4)
print avgdepth, avgpressure
return
```

# Program

main program: proga.c

> ********************************************************************
/*  Main Program: Computation of Pressure                 *
/*                                                               */
********************************************************************
/*  Defined Constants:                                     */
/*    count – number of data values for depth             */
/*                                                              */
/*  Input Variables:                                       */
/*    depth – depth of water in feet                      */
/*                                                              */
/*  Computed Variables:                                    */
/*    pressure – pressure in psi at different depths */
/*    avgdepth – average depth of water                    */