As the lines trailing comment #5 reveal, the first argument consists of the file handle identifier (`FILE`). The second argument provides a scalar identifier (`$DinosaurName`) to which you can assign the character string that the `read()` function retrieves from the file. The last (fourth) argument pertains to this identifier. Set at zero, this argument tells the `read()` function to use the zero index of the target identifier (`$DinosaurName`) as the starting position of the character string it copies to the identifier. Generally, then, this argument designates the position in the target string to which you want to transfer the string you copy from the file.

For the third argument of the `read()` function, you furnish the number of characters you want the `read()` function to retrieve from the file. To accomplish this, you use an expression that involves subtracting one dereferenced value from another. Here is the expression:

```
`$WordPositions{$Name}->[1]-1) - ($WordPositions{$Name}->[0])`
```

You use the `$Name` identifier to identify a given key (dinosaur name) in the `%WordPositions` hash. Using the key, you retrieve the array associated with the key. The array contains two elements. The first element (at index 0), provides the position of the first character of the dinosaur name. The second element (at index 1) tells you a position in the file one character beyond the end character of the dinosaur name. To obtain the length of the dinosaur name, you subtract 1 from the end and then subtract the beginning from the end. The difference informs the `read()` function how many characters it is to transfer from the file to the `$DinosaurName` identifier.

Given that you have assigned the name of a dinosaur to the `$DinosaurName` identifier, you then call the `join()` function to concatenate the dinosaur name with other dinosaur names into a single string, (`$FinalString`). As you concatenate the names, you insert a dash between the dinosaur names as a cosmetic feature.

After the `foreach` statement traverses all the names in the array, its block terminates, and you close the file stream. To close the file stream, you use the `close()` function (see comment #6). After that, you call the `print()` function and provide `$FinalString` as its only argument. Figure 14.11 displays the result.

![](bbox=[0.18, 0.701, 0.595, 0.888])

**Figure 14.11**  
Use the `read()` function to retrieve data and create a string you print to the monitor.