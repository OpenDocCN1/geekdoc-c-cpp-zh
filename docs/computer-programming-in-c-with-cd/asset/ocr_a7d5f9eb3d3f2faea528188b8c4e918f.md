```
```cpp
int incentive;

void getSalesPerson()
{
    cout<<"Enter incentive : ";
    cin>>incentive;
    cout<<endl;

}
void displaySalesPerson()
{
    cout<<"Incentive : "<<incentive<<endl;
}
};
class Officer: public Staff
{
public:
    char grade, department[15];
    int experience, salary;

    void getofficer()
    {
        cout<<"Enter department : ";
        cin>>department;
        cout<<endl;
        cout<<"Enter grade : ";
        cin>>grade;
        cout<<endl;
        cout<<"Enter experience (no. of years) : ";
        cin>>experience;
        cout<<endl;
        cout<<"Enter salary : ";
        cin>>salary;
    }
    void displayofficer()
    {
        cout<<"Department : "<<department<<endl;
        cout<<"Grade : "<<grade<<endl;
        cout<<"Experience : "<<experience<<endl;
        cout<<"Salary : "<<salary<<endl;
    }
};
class Regular: public SalesPerson
{
public:
    int experience, salary;
    void getRegular()
    {
        cout<<"Enter experience (no. of years) : ";
        cin>>experience;
```
```