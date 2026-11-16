```
{
    char name[50];
    char section;
    int roll;
};

int main()
{
    struct student s1;
    cout<<("Enter the name of student\n");
    cin.getline(s1.name,50);
    cout<<("Enter section of the student\n");
    cin>>s1.section;
    cout<<("Enter roll number of the student\n");
    cin>>s1.roll;
    fstream fout("student.txt",ios::out);
    if(fout==NULL)
    {
        cout<<("Can't open the file");
        return -1;
    }
    fout<<s1.name;
    fout<<'\n';
    fout<<s1.section;
    fout<<'\n';
    fout<<s1.roll;
    fout.close();
}
```