```
print "$NL Reference: \$RefToExtraVegetable -- ". $RefToExtraVegetable;
print "$NL Dereference: \$\$RefExtraVegetable -- ". $$RefToExtraVegetable;
print $NL . $DL;

#Array
print "$NL Array: $NL Value in \@Fruits -- @Fruits";
print "$NL Reference: \$RefToFruits -- ". $RefToFruits;
print "$NL Dereference: \@\$RefToFruits-- " ;
print "@$RefToFruits";

print $NL . $DL;

#Hash
print "$NL Hash: $NL Value in %Cereals -- ";
print %Cereals;
print "$NL Reference: \\\%Cereals -- ". \%Cereals;
print "$NL Dereference: \%\$RefToCereals -- " ;
print %$RefToCereals;
```

At comment #1 in Listing13_04, you set up three identifiers: a scalar, an array, and a hash. At
comment #2, you define references for each of the identifiers. In the lines following comment
#3, you print the values the non-reference identifiers store, the memory location of the reference,
and then the dereferenced values. You use the $ type identifier to dereference a scalar, a @ type
identifier to dereference an array, and a % identifier to dereference a hash. Figure 13.5 shows
you that the dereferenced values match the values stored in the standard identifiers.

![](bbox=[0.183, 0.652, 0.597, 0.892])

# Figure 13.5
Dereferencing a reference
involves using the type
identifier.