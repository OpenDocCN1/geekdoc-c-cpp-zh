# Example 4-17

```
```java
public class Student
{
    //Data members, data fields, or characteristics
    private int studentNumber;
    private string studentName;
    private int score1;
    private int score2;
    private int score3;
    private string major;

    //default constructor
    public Student()
    {
    }

    //constructor with one argument
    public Student(int sID)
    {
        studentNumber = sID;
    }

    //constructor with two arguments
    public Student(int sID, string name)
    {
        studentNumber = sID;
        studentName = name;
    }

    //constructor with six arguments
    public Student(int sID, string name,
        int s1, int s2, int s3, string maj)
    {
        studentNumber = sID;
        studentName = name;
        score1 = s1;
        score2 = s2;
        score3 = s3;
        major = maj;
    }

    //Properties
    public string StudentName
    {
        get
        {
            return studentName;
        }
    }
```
```