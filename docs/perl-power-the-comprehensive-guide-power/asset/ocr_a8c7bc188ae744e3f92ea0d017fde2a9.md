```
```perl
@CitiesInBrazilA = qw( Aracaju Brasilia Canoas Itabuna Manaus);
@CitiesInBrazilB = qw( Salvador Teresina Natal Curitiba);

$Itr = 1;
print "\n Brazilian city group A: \n";
foreach $City (@CitiesInBrazilA){
    print "\n " . $Itr++ . ". $City";
}

$Itr = 1;
print "\n\n Brazilian city group B: \n";
    foreach $City (@CitiesInBrazilB){
        print "\n " . $Itr++ . ". $City";
    }

#2 Two elements
#array to copy to, starting position, number of elements deleted, source array
print "\n\n Elements from B spliced into A; 2 deleted, following 2 in A: ";
print "\n " . 'Syntax splice (@CitiesInBrazilA, 2, 2, @CitiesInBrazilB);';
splice(@CitiesInBrazilA, 2, 2, @CitiesInBrazilB);

$Itr = 1;
foreach $City (@CitiesInBrazilA){
    print "\n " . $Itr++ . ". $City";
}
```
```

The lines accompanying comment #1 set up two arrays, @CitiesInBrazilA and @CitiesInBrazilB. The first consists of six city names, the second of four. Then you use for statements to iterate through the elements in the array. Following the definition and display of the arrays containing the cities, in the lines associated with comment #2, you call the splice() function to transfer the elements from @CitiesInBrazilB to @CitiesInBrazilA. Figure 6.11 illustrates the effects of the splice() operation.

As the lines trailing comment #2 reveal, the first argument to the splice() function is the destination array, @CitiesInBrazilA. Following the designation of the destination array, you then name the position after which you want to begin replacing elements. In this case, this element is the second, “Brasilia.” You then designate the number of elements in the destination