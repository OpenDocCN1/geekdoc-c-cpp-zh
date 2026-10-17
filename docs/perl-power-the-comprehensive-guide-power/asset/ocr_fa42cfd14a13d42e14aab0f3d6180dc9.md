```
$Record = $DinoRecords->[$Itr];
$NumOfFields = scalar(@$Record);
for(my $Itr = 0; $Itr < $NumOfFields ; $Itr++){
	printf(" %-20s", $Record->[$Itr]);
	}
}

#3 Work with formats. Set the fields to alpha length 2 - 20
$Record = "A3 A20 A20 A20";
$RecordLength = length(pack($Record));

print "\n\n Record length:" . $ RecordLength . "\n";

#4 Open a file to write to -- overwrites old data
open(FILE, "+>RecordData.txt") || die "\n\tCannot access file.";

#5 Write a record to the file
#Traverse both dimensions of the array
for($Itr = 0; $Itr < $Length ; $Itr++){
	print("\n");
	$Record = $DinoRecords->[$Itr];
	#Access each field ...
	$Field = 0;
	$DinoName = $Record->[$Field];
	$FamilyName = $Record->[$Field++];
	$Period= $Record->[$Field++];
	print(FILE pack("A3 A20 A20 A20", "\n",
		$DinoName,
		$FamilyName,
		$Period));
	}

close(FILE);

#6 Close and view the records
print "\n File created...";
system('notepad RecordData.txt');
```