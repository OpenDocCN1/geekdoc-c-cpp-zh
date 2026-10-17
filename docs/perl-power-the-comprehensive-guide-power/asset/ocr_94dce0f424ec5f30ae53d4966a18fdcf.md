# # CHAPTER 9 Extending Hash Applications

```
`%NewlandsElements = (H, D, Li, D, B, D, C, D, N, D, O, D, F, D, Na, D,
Mg, D, Al, D, Si, D, P, D, S, D, Cl, D, K, D,
Ca, D, Cr, D, Ti, D, Mn, D, Fe, D, Co, D, Ni, D,
Cu, D, Zn, D, Y, D, In, D, As, D, Se, D, Dr, D,
Rb, D, Sr, D, La, D, Ce, D, Zr, D, Nb, D, Mo, D, Ru, D,
Rh, D, Pd, D, Ag, D, Cd, D, U, D, Sn, D, Sb, D,
Te, D, I, D, Cs, D, Ba, D, V, D);`
```

```
`#3 use keys to extract the unique keys
$MLenK = scalar(keys(%MendeleevElements));
$MLenV = scalar(values(%MendeleevElements));
$NLenK = scalar(keys(%NewlandsElements));
$NLenV = scalar(values(%NewlandsElements));`
```

```
`#Display the result
printf("$DL");
printf("\n %-30s %-30s" , $COLAHEAD , $COLBHEAD);
printf("$DL");
printf("\n %-15s %-15s%-15s %-15s", "Keys" , "Values",
"Keys", "Values");
printf("$DL");
printf("\n %-15s %-15s%-15s %-15s", $MLenK, $MLenV ,
$NLenK, $NLenV);
system("pause");`
```

This program uses the same approach to the data and the presentation of the data that the two previous programs used. In the lines that comment #1 identifies, you set up formatting elements for the presentation table. At comment #2, you create two hashes. One, `%MendeleevElements`, holds keys and values for the data Mendeleev used. The second hash, `%NewlandsElements`, holds keys and values for the data Newlands used. The "D’s" designate “defined.”

At comment #3, you employ the `scalar()` function to determine the number of keys and values in each hash. The sole argument of the `keys()` function consists of the hash from which you want to access the keys. The return value of the `keys()` function consists of all the keys in an array. When you cascade the `keys()` function into the `scalar()` function, the result is a value representing the number of keys.