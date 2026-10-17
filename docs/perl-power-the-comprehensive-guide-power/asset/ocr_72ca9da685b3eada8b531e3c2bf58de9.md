```
# 2 Define the keys and values for a table
%Chemists = ("Trevisan", "Ancient alchemist",
            "Paracelsus", "Physician who cured diseases",
            "Priestley", "Discovered oxygen",
            "Lavoisier", "Father of modern chemistry",
            "Dalton", "Invented the atomic theory",
            "Woehler", "Father of organic chemistry",
            "Mendeleev", "Created the first table of elements",
            "Curies", "Isolated radium",
            "Thomson", "Discovered the electron"
           );

#3 Print the table
printf("$DL");
printf("%s", $NL . $TableTitle);
printf("$DL");
printf("\n %-15s %-20s", $COLAHEAD, $COLBHEAD);
printf("$DL");

# 4 Use each to retrieve key - value pairs
    while(($Name, $Achievement) = each(%Chemists)){
        printf("\n %-15s %-20s", $Name , $Achievement);
    }
```

The lines that comment #1 identify create elements that you can use to format a table. To create the string that the $TableTitle identifier contains, you form a string consisting of three parts. The first and third parts are padding. The second part is the string you want to use for a title. To create the padding parts, you subtract the length of the string used for the title of the table from the width of the table. You divide the remainder by two so that you can pad the title on either side. You then concatenate the parts using sprintf() and assign it to $TableTitle.

The lines trailing comment #2 define a hash, %Chemists, that contains keys identifying famous chemists and values that name their greatest accomplishments. At comment #3 you print the table header. To accomplish this, you print the title line you have assigned to $TableTitle and follow with the column headers.

At comment #4, you use a while control statement to iterate through the hash. To access the key-value pairs in the hash, you employ the each() function. You assign the return value of the each() function to a list of two scalars, $Name and $Achievement. Notice that you separate the scalars using commas. You assign the return value from the each() function to