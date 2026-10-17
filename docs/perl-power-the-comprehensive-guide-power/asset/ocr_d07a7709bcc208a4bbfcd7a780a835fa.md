# # The pack() Function

The `pack()` function allows you to create a fixed-length record by specifying the data types to be processed and the number of bytes needed to accommodate the data. To create fixed-length records, you first need to establish the length of the record you want to create. Suppose for starters that you want to write records that consist of the following fields:

Dinosaur Name Dinosaur Family Period of Existence

After surveying the basic data, you decide that you are safe if you use the following maximum lengths for the three fields that constitute the record:

20 characters 20 characters 20 characters

To create a record to accommodate these fields, you use the following approach:

$Record = "A20 A20 A20";
my $RecordLength = pack($Record);

The `pack()` function retrieves the information the `$Record` identifier provides and “packs” it into a single value. The resulting record length for the specifications provided is 60. Now you can use this record definition to write records to a file. Listing14_08 explores this activity in a context that allows you to create a file that contains fixed-length records. The program creates the file every time you execute it and opens the file using Notepad so that you can view it.

```
#Listing14_08
#1 Create anonymous embedded arrays
$DinoRecords = [
	[ #Container array
	['Parasaurolophus', 'Hadrosaurids', 'Late Cretaceous'],
	['Tsintaosaurus', 'Hadrosaurids', 'Late Cretaceous'],
	['Allosaurus', 'Carnosaurs', 'Late Jurassic'],
	['Centosaurus', 'Carnosaurs ', 'Late Jurassic',]
	];
#2 Print the records to preview them
#Dereference
@Ref = @$DinoRecords;
#Obtain the number of items in the container array array
$Length = scalar(@Ref);
#Traverse both the array and print its content
for($Itr = 0; $Itr < $Length ; $Itr++){
	print("\n");
}
```