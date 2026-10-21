```
NoOfRecords++;
}
MarkStatus.open((Marks::FileName+"Status").c_str(), ios::in | ios::out);
if(!MarkStatus.is_open())
{
 perror("Mark status file: ");
 exit(0);
}
cout << endl;
Marks::Session1Entered = MarkStatus.get();
Marks::Session2Entered = MarkStatus.get();
MarkStatus >> Marks::Practical1Entered;
MarkStatus >> Marks::Practical2Entered;
MarkStatus >> Marks::PresentationEntered;
// Now printing it
cout << PrintHeading << PrintMarkSheetHeading << PrintLine << PrintLine;
int i;
for(i = 0; i < NoOfRecords; i++)
{
 cout << StudMarks[i];
}
};
```

# Output

The following screenshots depict one specific run of the program.

```
Select Telnet 128.66.203.701
[lht@pgana ~]$ ./a.out
1. Enter Subjects
2. Enter Marks
3. Display Marks for a given subject for specific year
4. Exit
1
How Many Subjects? 3
Enter Subject No: 1
Enter Name: C++
Enter Subject No: 2
Enter Name: ComputerNetworks
Enter Subject No: 3
Enter Name: NetworkSecurity
1. Enter Subjects
2. Enter Marks
3. Display Marks for a given subject for specific year
4. Exit
2
```

> Fig. A.1 Screen 1 of output