# Figure 6.13

Use the splice() function to replace selected elements.

![](bbox=[0.387, 0.109, 0.829, 0.309])

# Remove a Range of Elements

Splice can be used to remove a range of elements from an array. In this version of the splice function, you employ only three argument. These arguments designate the array on which you want to perform operations, the position in the array after which you want to remove elements, and the number of elements you want to remove. Listing06_14 revisits one of the arrays of cities from the previous examples.

```
```perl
#Listing06_14

#1 Set up arrays
@CitiesInBrazilA = qw( Aracaju Brasilia Canoas Itabuna Manaus);
$Itr = 1;
print "\n Brazilian city group A: \n";
foreach $City (@CitiesInBrazilA){
        print "\n  " . $Itr++ . ". " . $City";
}


#2 Remove two elements
# Identify the array, the starting position, number of elements
print "\n\n" . 'splice (@CitiesInBrazilA, 2, 2);';
print "\nRemove two elements following position 2: \n";
#extract two elements after element two
splice (@CitiesInBrazilA, 2, 2);
#view the result
$Itr = 1;
foreach $City (@CitiesInBrazilA){
        print "\n  " . $Itr++ . ". " . $City";
}
```
```