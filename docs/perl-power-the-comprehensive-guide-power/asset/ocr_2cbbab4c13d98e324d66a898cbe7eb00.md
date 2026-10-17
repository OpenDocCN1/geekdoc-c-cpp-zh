# Converting a String into a Hash

```
```perl
$ListLength = scalar(@ElementList); #read length of array
print "\nNumber of items : $ListLength\n";

# 3 At the colons, separate the elements and melting points
# The expression calls for a colon with no spaces
foreach $Item (@ElementList){
    ($Element, $MeltingPt) = split(":",$Item );
        # Two steps that could be one: create a hash with the two parts
        $NewElementList{$Element} = $MeltingPt;
}#end foreach
# 4 Print the hash as a string; use each to retrieve keys and values
print "\nThe element list follows:\n";

$Itr = 1;
while (($Element, $MeltingPt) = each(%NewElementList)){
    printf "\n %-4s %-25s %-10.0f", $Itr++, $Element, $MeltingPt;
}#end while
```
```

The lines accompanying comment #1 in Listing09_05 create a string that consists of a number of chemical elements and their melting points. Commas separate the element-temperature pairs that constitute the string. To display this program in this book, it is necessary to break the string into a set of concatenated elements. You can derive a lesson from this. It remains essential not to introduce newline characters into a string you want to split. The `split()` function usually processes your string, but unless you tell it otherwise, it assumes you want to leave escape sequences alone. This can create problems.

In the lines comment #2 designates, you use the `split()` function to divide the string into items that consist of the element-value sets. To divide the string, you supply as a first argument to the `split()` function a comma followed by a blank space. You enclose these in double quotation marks. (You can also use forward slashes (`//`), the `q()` function, the `qq()` function, or single quotation marks.) The `split()` function returns the items that result when the string is divided as stipulated, and you assign these items to an array, `@ElementList`. You use the `scalar()` function to ascertain the number of items in the array, and as Figure 8.14 shows, you print this so that you can check the displayed elements against it.

At comment #3, you employ a `foreach` control statement to traverse the items in the `@ElementList` array. The `foreach` statement allows you to access each item in the array and assign it to a scalar, `$Item`. Within the `foreach` block, you then again use the `split()`