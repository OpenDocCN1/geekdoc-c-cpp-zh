# # Mineral Luck Using while and Selection Statements

```
unless(lc($ControlChar) eq 'g'){ #last exits the program
    last;
}
$Score = 1; #rest the score
system(cls);
next; #back to the top of the loop
}
#5 Isolate processing in the loop for the winning event
if($Score == 12){
    print "$NL You Win!!!!!."\n";
    print "$NL Press <Enter> for a new game or \\'q\' to quit. ";
    $ControlChar = <STDIN>;
    chomp($ControlChar);
    if(lc($ControlChar) eq 'g'){ #last exits the program
        last;
    }
    $Score = 1; #reset the score
    system(cls);
    print "$DL $NL The Mineral Name game. How's your luck? $DL $NL";
    next; #back to the top of the loop
}}
#end while
#6 An example of how to write a function.
sub enterData{
    print "$NL Score now $Score. ";
    $Score++;
    print "$DL";
    print "$NL Press <Enter>.\n";
    $ControlChar = <STDIN>;
}
```

In the lines trailing comment #1 in Listing11_11, you set up a hash that contains the names of minerals and their corresponding descriptions. You also create a number of identifiers to help with text formatting details. Using the `sprintf()` function, you cast the ASCII value of 240 to create the triple-dashed character you see in Figure 11.17. You also call `srand`. In this context, this is largely unnecessary, but `srand` supplements the `rand()` function and allows it to generate unique values.