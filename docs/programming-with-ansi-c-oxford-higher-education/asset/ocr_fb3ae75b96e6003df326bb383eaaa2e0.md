```
```
} else
{
	for(i = 0; i < NoOfRecords; ++i)
	{
		cout << StudMarks[i];
		NewMarksFile.write((char *) &StudMarks[i], sizeof(Marks));
		if(!NewMarksFile)
			perror("Error writing the new marks file: ");
		cout << endl;
	}
}
NewMarkStatus << Marks::SessionallEntered;
if(!NewMarkStatus)
	perror("Error writing the status file: ");
cout << endl;
NewMarkStatus << Marks::Sessionall2Entered;
if(!NewMarkStatus)
	perror("Error writing the status file: ");
cout << endl;
NewMarkStatus << Marks::Practical1Entered;
if(!NewMarkStatus)
	perror("Error writing the status file: ");
cout << endl;
NewMarkStatus << Marks::Practical2Entered;
if(!NewMarkStatus)
	perror("Error writing the status file: ");
cout << endl;
NewMarkStatus << Marks::PresentationEntered;
if(!NewMarkStatus)
	perror("Error writing the status file: ");
cout << endl;
NewMarkStatus << Marks::Subject;
NewMarkStatus << Marks::Year;
cout << "\n The mark status is \n";
cout << Marks::Subject;
cout << Marks::Year;
cout << Marks::SessionallEntered;
cout << Marks::Sessionall2Entered;
cout << Marks::Practical1Entered;
cout << Marks::Practical2Entered;
cout << Marks::PresentationEntered;
cout << endl;
}
ostream & PrintHeading(ostream & TempOut)
```
```