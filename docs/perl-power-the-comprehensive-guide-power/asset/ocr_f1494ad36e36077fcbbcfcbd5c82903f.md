# CHAPTER 8  Hashes

```
# 3 Use printf
print "\n 3. Use printf and %s to extract keys and values: \n";
printf(" %s - %s , %s - %s, %s - %s ", %Elements);
```

```
#4 Assign the implicit form of the hash to an array
print "\n 4. Assign the hash to an array and print: \n";
#Print the array -- See subsequent sections
@ElementArray = %Elements;
print "\n Listed: @ElementArray";
print "\n ... or on separate lines: \n";
foreach $LocVal (@ElementArray){
        print "\n " . $LocVal;
}
```

```
print "\n 5. Far-fetched formatting:\n ";
print "\n 5. Far-fetched formatting:\n ";
foreach $LocVal (@ElementArray){ #read to end of array
    if($Flag == 0){
        printf ("\n Element %-15s", $LocVal); #left align 15 char
        $Flag = 1; #reset flag
        next; #skip the rest of the foreach loop
    }
    if($Flag == 1){
        printf ("Symbol %-25s", $LocVal);
        $Flag = 0; #reset flag
    }
}
```

Figure 8.4 illustrates the output of Listing08_03. In the lines that accompany comment #1, you use the lookup form of the hash to access the value of a given key. You place the key of the hash element between the curly braces. In this way, you retrieve the value the hash element contains.

At comment #2, you use a crude approach to printing the contents of an array as a list. This approach provides you with a way to confirm the contents of a hash, but it proves unwieldy if you are dealing with a large collection of elements.