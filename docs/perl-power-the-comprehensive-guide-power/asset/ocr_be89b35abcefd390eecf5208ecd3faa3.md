# # CHAPTER 7 Arrays and Data Containers

```
```perl
#print the customers
print "$LINE \n \n Sally: \n \n ";
for($Itr = 0; $Itr < scalar(@SallyCustomers); $Itr++){
    print " \n ". $Itr + 1 . " ". $SallyCustomers[$Itr] . " ";
}
print "$LINE \n \n Chu: \n \n ";
for($Itr = 0; $Itr < scalar(@ChuCustomers); $Itr++){
    print " \n ". $Itr + 1 . " ". $ChuCustomers[$Itr] . " ";
}
print "$LINE \n \n Caesar: \n \n ";
for($Itr = 0; $Itr < scalar(@CaesarCustomers); $Itr++){
    print " \n ". $Itr + 1 . " ". $CaesarCustomers[$Itr] . " ";
}
print "$LINE";
print "\n \n\n";

#5 Check for whether to refresh the display
if($ScheduledCustomers >= 3){
    sleep(1.0);
    print "\n\n";
    system("cls");

    # print "$LINE";
    print "\n \n \n Thank you for your patience.";
}

#6 Exit when done
if($ScheduledCustomers == 0){
    print "\n\n";
    exit(0);
}
}
```
```