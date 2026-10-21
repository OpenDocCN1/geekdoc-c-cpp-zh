# PROGRAM 9.7 Multiple inheritance

```
//MultipleInheritance.cpp
#include <iostream>
#include <string>
using namespace std;
const int Sports = 3;

// First base class
class student
{
private:
    string Name;
    string Address;
    char Grade;
    string NameofSchool;
public:
    student(string TempName, string TempAddress, char TempGrade,
    string TempNameofSchool)
    {
        Name = TempName;
        Address = TempAddress;
        Grade = TempGrade;
        NameofSchool = TempNameofSchool;
    }
};

// Second base class
class SportsPerson
{
private:
    string Sport;
    string DetailsOfEvents;
    string Experience;
    int Age;
public:
    SportsPerson(string TempSport, string TempDetailsOfEvents, string TempExperience, int TempAge)
    {
        Sport = TempSport;
        DetailsOfEvents = TempDetailsOfEvents;
        Experience = TempExperience;
        Age = TempAge;
    }
};

// Derived class
class SportsStudent : public SportsPerson, public student
{
private:
    string SportsSubjects[Sports];
    int SportsPoints;
public:
    SportsStudent(string TempName, string TempAddress, char TempGrade, string TempNameofSchool,
    string TempSport,
    string TempDetailsOfEvents, string TempExperience, int TempAge,
    int TempSportsSubjects[], int TempSportsPoints) :
    student(TempName, TempAddress, TempGrade, TempNameofSchool),
    SportsPerson(TempSport, TempDetailsOfEvents, TempExperience, TempAge)
```