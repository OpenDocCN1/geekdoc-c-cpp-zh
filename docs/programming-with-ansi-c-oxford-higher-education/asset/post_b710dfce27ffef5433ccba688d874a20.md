
{
    TempOut << setw(30) << setiosflags(ios::right);
    TempOut << "Marks for subject" << setw(20) << Marks::Subject << endl;
    TempOut << setw(30) << setiosflags(ios::right) << "for the year" << setw(20) <<
    setiosflags(ios::right) << Marks::Year << endl;
    return TempOut;
}
ostream & PrintMarkSheetHeading(ostream & TempOut)
{
    TempOut << setw(12) << setiosflags(ios::left) << setiosflags(ios::fixed) <<
    setprecision(2) << setiosflags(ios::showpoint);
    TempOut << "Roll number" << setw(12) << "Sessional1";
    TempOut << setw(12) << "Sessional2";
    TempOut << setw(12) << "Practical1";
    TempOut << setw(12) << "Practical2";
    TempOut << setw(12) << "Presentation";
    return TempOut;
}
ostream & PrintLine(ostream & TempOut)
{
    TempOut << endl << "      ";
    TempOut << endl;
    return TempOut;
}
void DisplayMarks()
{
    cout << "Please specify the subject \n"; cin >> Marks::Subject;
    cout << "Please specify the year \n";
    cin >> Marks::Year;
    char *StringYear = itoa(Marks::Year, 10);
    Marks::FileName = "Marks" + Marks::Subject + StringYear;
    fstream MarksFile(Marks::FileName.c_str(), ios::in | ios::out | ios::binary);
    fstream MarkStatus((Marks::FileName + "Status").c_str());
    if(!MarksFile.is_open())
    {
        cout << "Marks file for the year that you have specified does not exist.";
        cout << "\n Make sure the file exists\n";
        exit(0);
    }
    vector <Marks> StudMarks;
    Marks DummyMarks;
    int NoOfRecords = 0;
    while(MarksFile.read((char *) &DummyMarks, sizeof(Marks)))
    {
        StudMarks.push_back(DummyMarks);
    }
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

Screen 1 This shows the subject detail entry and ends with a selection for entering marks for a subject.

![](img/0da15892b2796544fb447dc5727e9ab4_630_0.png)

# Fig. A.2 Screen 2 of output

Screen 2 This screen begins with the query for the subject name and year. The default is OOCP and 2007. It asks for the number of subjects and a subject and starts marks entry.

![](img/0da15892b2796544fb447dc5727e9ab4_630_1.png)

# Fig. A.3 Screen 3 of output

Screen 3 This shows the marks of each student in a matrix form, displays mark status, and loops back to the menu where the user chooses to enter the marks once again.

![](img/0da15892b2796544fb447dc5727e9ab4_630_2.png)

# Fig. A.4 Screen 4 of output

Screen 4 The user is prompted again for the subject and marks; the program displays the marks that are entered and are not.

![](img/0da15892b2796544fb447dc5727e9ab4_631_0.png)

# Fig. A.5 Screen 5 of output

Screen 5 Marks are displayed in the matrix form after the entry.

![](img/0da15892b2796544fb447dc5727e9ab4_631_1.png)

# Fig. A.6 Screen 6 of output

Screen 6 The loop comes back to ask for entry and shows the status of the specific subject with specific year.

# Fig. A.7 Screen 7 of output

Screen 7 The practical marks are entered and information is displayed.

```
Select Telnet 128.66.203.201
The Mark Status is
C++2012ynnn
1. Enter Subjects
2. Enter Marks
3. Display Marks for a given subject for specific year
4. Exit
2
Do You want to enter marks for subject other than 00CF for year 2007?
Total subjects are 3
1. C++
2. ComputerNetworks
3. NetworkSecurity
Please Enter your choice1
Please Enter the year
2012
MarksC++2012
Welcome to Marksheet Entry System!
Status read from file is
Subject is C++
Year is 2012
Sessional 1 Marks are available
Sessional 2 Marks are available?
Practical 1 Marks are yet to be entered
Practical 2 Marks are yet to be entered
```

```
Select Telnet 128.66.203.201
Presentation Marks are yet to be entered
Please Enter Marks one by one
1. First Sessional Marks
2. Second Sessional Marks
3. First Practical Marks
4. Second Practical Marks
5. Presentation Marks
3
Enter Marks For Roll Number 1 11
Enter Marks For Roll Number 2 12
Enter Marks For Roll Number 3 13
Enter Marks For Roll Number 4 13
Enter Marks For Roll Number 5 11
1 12 34 11 0 0
2 15 35 12 0 0
3 23 37 13 0 0
4 17 34 13 0 0
5 29 33 11 0 0
```

![](img/0da15892b2796544fb447dc5727e9ab4_633_0.png)

Fig. A.8 Screen 8 of output

Screen 8 The marks are entered and looped back.

![](img/0da15892b2796544fb447dc5727e9ab4_633_1.png)

Fig. A.9 Screen 9 of output

Screen 9 Practical second test marks are entered as shown.

# Fig. A.12 Screen 12 of output

Screen 12 Complete marks are entered.

# Fig. A.13 Screen 13 of output

Screen 13 The final mark sheet is printed.

## A.4 EXPLANATION

The program begins with two important definitions. One is a function for getting a string from an int value. There is a function itoa available in Windows or TC++, but it is not available in Linux. We need such a function to run the program under Linux.¹

The other definition is an enum, which describes the reading status. We have already seen that the program may be reading marks about any head at any given point of time. It is enum that tells us what we are reading.

Then, we have the most important class of our program, namely, Marks. The members of the class are divided into two parts. Static members represent the metadata about the class, whereas other members are integers representing the different heads of marks of a student. We have our static members defined and given default values outside the body of the class. It is important to note that the name of the file is a concatenation of three strings. The first string is always ‘Marks’, the second is the subject for which the data entry is made, and the third is the string representation of the year value. Thus, this makes the name of the file unique for each subject for each year. For example, the file name could be Marks00CP2007, MarksAI2008, etc.

These files cannot store their metadata. We need an additional file to store the same. We name that file as the original filename plus the word ‘Status’. Thus, status files for the given two cases will be Marks00CP2007Status and MarksAI2008Status. These are long but unambiguous names.

It is interesting to see that the argument requires a C-type string; hence, we need to call c_str() function with the file name to get the C-type string from a string object.

Next is the Subject class. This class stores only two bits of information, the subject name and number. Ideally, it should also store the name of the file for each subject where syllabus is stored for that subject.

It is needless to state the importance of the overloaded << and >> operators for both the classes and that we have proper constructors for them as well.

Next is the function ChooseSubject(). This is an important function, which reads from the SubjectFile and lets us choose the subject. The following statements are worth having a look.

```
while(!SubjectFile.eof())
{
    int TempNo;
    string TempName;
    SubjectFile >> TempNo;
    SubjectFile >> TempName;
    NoOfSubjects++;
    Subject MCA_Subject_In(TempNo, TempName);
}
```

¹ This function has been taken from the web. The website and the author’s name have been specified in the program itself. As programmers need to invest time and energy to program and debug various cases, it is always a viable option to look for readymade solutions on the web and incorporate them in a program. The advantage of such solutions is that they are usually tested and designed for generic cases. Incorporating such codes makes the program more robust and generic. One must carefully look at the copyright warnings in such cases though.
