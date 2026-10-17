# CHAPTER 7 } Arrays and Data Containers

**Figure 7.6**
As the `shift()` function is called, elements are removed from the head of the array.

![](bbox=[0.395, 0.11, 0.822, 0.306])

# Inserting Elements into the Front of an Array

The `unshift()` function performs an action that is the reverse of the `shift()` function. Rather than removing the first element in an array, the `unshift()` function inserts an element into the first or zero position of an array. Consider Figure 7.7. When the `unshift()` function inserts a new element into an array, the indexes of the existing elements increase in value by one. They are “unshifted” from the front or head of the array toward its tail or end.

**Figure 7.7**
The `unshift()` function moves all the elements further from the head of the array when it adds a new element.

![](bbox=[0.426, 0.487, 0.797, 0.654])

Listing07_06 explores the fundamental use of the `unshift()` function.

```
```perl
#Listing07_06
#1 Set up an array of Russian cities
@CitiesInRussia = qw(Kaluga Kazan Penza Ufa);

print "\n Cities in Russia: ";
for ($Itr = 0; $Itr < scalar(@CitiesInRussia); $Itr++){
    print "\n " . $Itr . ". " . $CitiesInRussia[$Itr];
}
```
```