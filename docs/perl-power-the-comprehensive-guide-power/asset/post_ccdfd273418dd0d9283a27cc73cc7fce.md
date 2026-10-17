
## CHAPTER 6 Array Fundamentals

```perl
@SomeArrayA = (@SomeArrayA, "Little");
@SomeArrayA = (@SomeArrayA, "things", "always");
@SomeArrayA = (@SomeArrayA, "matter", "in", "the", "end");
```

In each case, you assign the array back to itself as you populate it. No element is lost through the repeated list assignment operations.

With both the scalar and implicit (@) identifiers, when you assign values to arrays, you do not need to worry about data types. You can assign both numbers and strings. Certainly, in many respects, as with the creation of undefined value through arbitrary assignments, mixing array values can create problems. However, it remains that Perl arrays have no strict data types, so you can add whatever elements you want. Consider the following use of the list operator from Listing06_01:

```perl
@MixedArray = (32, all, 22, 44.7, 32, 34.5, numbers);
```

Each element is associated with an index. You can retrieve the value from the array using the index. The value the element possesses when you retrieve it from the array depends on how you use it. If you do not use the value in a specific way, it is displayed as a string value. Here are the values that display when you employ the print() function to print the interpolated elements:

```text
Mixed array: 32 all 22 44.7 32 34.5 numbers
```

### Retrieving and Printing Values

To retrieve a value using the scalar identifier, you employ the index of the value you want to retrieve. As shown in the lines associated with comment #2 in Listing06_01, you can concatenate it with an interpolated string or print it as a scalar value. For the item just assigned to index 1, you use the following statements:

```perl
print "$NL Array element identified by index 1: " . $NewArray[1] . "$NL";

print "$NL Array element identified by index 1: $NewArray[1] $NL";
```

As Figure 6.2 illustrates, when the interpreter processes these statements, you see the following output for both statements:

```text
Array element identified by index 1: all
```

In the previous list assignment, 32 was assigned to the 0 index. The word all was assigned to the 1 index. As you add them to your array, the values you add are assigned to the next available index. To retrieve values for display, you can use the print() command and the index form of the array:

### Basics of Arrays

```perl
print "$NL Mixed array [0]: ". $MixedArray[0];
print "$NL Mixed array [1]: ". $MixedArray[1];
```

The output is as follows:

```text
Mixed array [0]: 32
Mixed array [1]: all
```

To print all of the elements in an array, you use the `print()` function in conjunction with double quotes (or the `qq()` function). The contents of the array display at the terminal. Consider the following statement:

```perl
print "$NL Elements after list add: ". "@SomeArrayA";
```

Given that you have populated `@SomeArrayA` as previously shown, you see the following output:

```text
Elements after list add: Little things always matter in the end
```

### Context and Retrieval

When you retrieve a value from an array, the operations you use on it determine what it means. If you want to retrieve a value from an array as a number, for example, you can extract it by assigning it to a scalar identifier that you then use as a number. You can also extract a value from an array as part of a math operation. As Figure 6.2 illustrates, here is an example of an extraction that results in the conversion of the numbers in arrays to scalars suitable for an addition operation:

```perl
$AddedValues = $MixedArray[0] + $MixedArray[3];
```

Using the `print()` function to print the resulting value, you see the following output:

```text
Added Value 76.7
```

Figure 6.2 illustrates the output of Listing06_01.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_151_0.png)

**Figure 6.2** Use determines the form items assume when you retrieve them from an array.

### Problems with Initialization

Implicit declaration of an array identifier does not initialize an array with values. The same can be said of defining an array in the scalar form. If you do not assign values to an array, the elements of the array remain undefined. To explore how this is so, consider the lines associated with comment #1 in Listing06_02, in which you declare an implicit (@ImplicitArray) and an array using the scalar ($NewArray[20]) syntax.

```perl
#Listing06_02
# Array definition issues
$NL = "\n";
#1 Declare identifiers
@ImplicitArray; # Array as array
$NewArray[20]; # Array as a scalar
#2 Test for definition
$LenA = @NewArray;
print "$NL Non-initialized array length of \$NewArray[20]: " . $LenA;
$LenA = @ImplicitArray;
print "$NL Non-initialized array length of \@ImplicitArray: " . $LenA;
#3 Arbitrary definitions more or less successful
$NewArray[15] = 40;
$LenA = scalar(@NewArray);
print "$NL 3.A Initialized (\@) array length: " . $LenA;
$NewArray[20] = 40;
$LenA = scalar(@NewArray);
print "$NL 3.A Initialized (\@) array length: " . $LenA;
print "$NL 3.A Elements in the array: @NewArray";
print "$NL 3.A Value at 15: $NewArray[15]";
print "$NL 3.A Value at 20: $NewArray[20]";
print "$NL";
if(defined ($NewArray[15])){
    print "$NL 3.B Value DEFINED for 15.";
}
if(!defined($NewArray[15])){
    print "$NL 3.B Value NOT DEFINED for 15.";
}
if(defined ($NewArray[18])){
    print "$NL 3.B Value DEFINED for 18.";
}
if(!defined($NewArray[18])){
    print "$NL 3.B Value NOT DEFINED for 18.";
}
if(defined ($NewArray[20])){
    print "$NL 3.B Value DEFINED for 20.";
}
if(!defined($NewArray[20])){
    print "$NL 3.B Value NOT DEFINED for 20.";
}
print "$NL";

#4 Initializing each element
$LENGTH = 20;
# implicit using list
@NewArrayA = (1 .. $LENGTH);
# Scalar using a for statement
for($Itr = 0; $Itr < $LENGTH; $Itr++){
    $NewArrayB[$Itr] = 0;
}

# Explorations
$LenA = scalar(@NewArrayA);
$LenB = scalar(@NewArrayB);

print "$NL 3.C Initialized (\@NewArrayA) array length: " . $LenA;
print "$NL 3.C Initialized (\@NewArrayB) array length: " . $LenB;
print "$NL";
print "$NL 3.C \@NewArrayA value at 15: $NewArrayA[15]";
print "$NL 3.C \@NewArrayB value at 15: $NewArrayB[15]";
print "$NL";
print "$NL 3.C All values \@NewArrayA: \n @NewArrayA";
print "$NL 3.C All values \@NewArrayB: \n @NewArrayB";
print "$NL";
```

To see that the space indicates undefined elements, you implement a series of `if` statements that use the `defined()` function. You select index values of 15, 18, and 20 to test. As Figure 6.3 shows, while the array supposedly contains 20 elements, the value of index 18 remains undefined.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_155_0.png)

You also print values from the two arrays. In both cases, the output reveals that values are stored in the elements of the array. You see a value of 15 for the array implicitly initialized, and you see a value of 0 for the array you initialized using its scalar form. You can then also display the contents of the two arrays and see that values have been assigned to each index. Finally, you can also subject the two arrays to tests that involve iterating through all their elements using the `defined()` function to verify their definitions. In this way, you see that values reside at each index for the two arrays.

You can assign one array to another, and you can concatenate lists. In the previous section, you used the list function to add individual scalar items to an array. You can also use the list function to concatenate an array with one or more other arrays. Listing06_03 illustrates several such operations.

```perl
#Listing06_03
#1 List initialization
@StateArrayA = ("New York", "Texas", "California");
print "\n First list: @StateArrayA";

#2 Assignment of one list to another
@StateArrayB = @StateArrayA;
print "\n" . ' Printed as @StateArrayB: ' . "@StateArrayB";

#3 Two arrays can be concatenated using the list function.
@StateArrayC = ("Delaware", "Vermont", "Maine");
print "\n Create a third array: @StateArrayC ";

#4 concatenated arrays
@StateArrayD = (@StateArrayA, @StateArrayC);
print "\n Concatenate A and C to form array D: \n @StateArrayD";

$DLength = @StateArrayD;
print "\n Length of array D: $DLength \n";

#5 Access elements for iterative display
print "\n Ways to iterate through the elements in an array \n";
print "\n Use a for loop for the \$ identifier of array D: ";
for($Itr = 0; $Itr < $DLength; $Itr++){
    print "\n " . $Itr . " . $StateArrayD[$Itr]";
}

print "\n Use a foreach loop for the @ identifier of array D: ";
$Itr = 0;
foreach $State (@StateArrayD){
    print "\n " . $Itr++ . " . $State";
}
```

At comment #1 in Listing06_03, you initialize @StateArrayA using a list. In the lines trailing comment #2, you assign @StateArrayA to @StateArrayB and then print
