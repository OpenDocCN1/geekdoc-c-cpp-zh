```
class Total :public Internal, public External
{
    int total_marks;
public :
    void input()
    {
        input_sub();
        input_im();
        input_em();
    }
    void show()
    {
        show_sub();
        show_im();
        show_em();
        total_marks = i_marks + e_marks;
        cout << "\tTotal Marks=" << total_marks << endl;
    }
};
void main()
{
    clrscr();
    Total tm;
    tm.input();
    cout << "\n\t + + + + + + + + +Student Report+ + + + + + +\n" << endl;
    tm.show();
    getch();
}
```

# OUTPUT :

Enter student name
Hari Pandey
Enter the roll number
1001
Enter the subject name
OOP In C++
Enter internal marks (0 to 20)
18
Enter External marks (0 to 80)
75
+ + + + + + + + +Student Report+ + + + + + +