# # 386 Programming with ANSI C++

```
```cpp
student(string TempName, string TempAddress, char TempGrade, string TempNameOfSchool)
{
 Name = TempName;
 Address = TempAddress;
 Grade = TempGrade;
 NameOfSchool = TempNameOfSchool;
};
// Derived class
class ScienceStudent : public student
{
 int marks[Science];
 string ScienceName;
 string PractSchedule;
public:
 ScienceStudent(string TempName, string TempAddress, char TempGrade, string TempNameOfSchool, int TempMarks[], string TempScienceName, string TempPractSchedule):
 student(TempName, TempAddress, TempGrade, TempNameOfSchool)
 {
 for(int i = 0; i < Science-1; i++)
 marks[i] = TempMarks[i]; ScienceName = TempScienceName; PractSchedule = TempPractSchedule;
 }
};
// Further derivation from the derived class
class GUScienceStudent : public ScienceStudent
{
 string ScienceProjectDetails;
 string GuideName;
 string SubjectsOpted[2];
public:
 GUScienceStudent(string TempName, string TempAddress, char TempGrade, string TempNameOfSchool, int TempMarks[], string TempScienceName, string TempPractSchedule, string TempScienceProjectDetails, string TempGuideName, string TempSubjectsOpted[])
 : ScienceStudent(TempName, TempAddress, TempGrade, TempNameOfSchool, TempMarks, TempScienceName, TempPractSchedule)
 {
 ScienceProjectDetails = TempScienceProjectDetails;
 GuideName = TempGuideName;
 for(int i = 0; i < OptionalSubjects; i++)
 SubjectsOpted[i] = TempSubjectsOpted[i];
 }
};
void main()
{

```