# Mastering the SAS DS2 Procedure: Advanced Data Wrangling Techniques

6. The sixth parameter, duplicate, determines whether to ignore duplicate keys when loading a table into the hash package. Valid values are 'add', 'replace' and 'error'. The default is 'add', which stores the first key value and ignores all subsequent. 'Replace' causes duplicates to replace the original key values, which results in the last being the only one retained. 'Error' reports an error in the SAS log if a duplicate key is found.

```
dcl package hash h1(
  [SupplierID],[SupplierName SupplierAddress Country],l
  'crs.supplier', 'a', 'error');
```

7. The seventh parameter, suminc, specifies a variable that maintains a summary count of hash package keys. Because we won't be using this feature in our demo, we'll just provide a null value

```
dcl package hash h1(
  [SupplierID],[SupplierName SupplierAddress Country],l
  'crs.supplier', 'a', 'error', 'no');
```

8. The last parameter, multidata, specifies whether multiple data items are allowed for each key. Valid values are 'multidata', 'yes' or 'y', which specify that multiple data items are allowed for a key, or 'singledata', 'no' or 'n', which specifies that multiple data items are not allowed for a key. The default is 'no'. Because duplicates are not expected, we have skipped defining this parameter in our example but to explicitly provide a 'no' value for clarity:

```
dcl package hash h1(
  [SupplierID],[SupplierName SupplierAddress Country],l
  'crs.supplier', 'a', 'error', 'no');
```

Alternatively, the hash object can be partially constructed on instantiation, and hash package methods used to subsequently load constant data and define the key and data values. Because these values need to be set only once before we use the hash object, the INIT method would be an excellent choice for making these assignments:

```
dcl package hash h1();
method init();
/* The hash object definition is completed via method calls*/
h1.keys((SupplierID));
h1.data((SupplierName SupplierAddress Country));
h1.hashexp(1);
h1.dataset('crs.supplier');
h1.ordered('a');
h1.duplicate('error');
h1.multidata('no');
h1.definedone();
end;
```

# 5.3.2.2 Using a Hash Object as a Lookup Table

We will use the code from the previous section to instantiate a hash object and then use the object's FIND method to retrieve data base on the key. FIND produces a return code-0 if the