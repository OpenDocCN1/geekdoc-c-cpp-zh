```
char lname[20];
long int recsize;

fp=fopen("EMP.DAT","rb+");
if(fp==NULL)
{
    fp=fopen("EMP.DAT","wb+");
    if(fp==NULL)
    {
        printf("
Can't Open File");
        exit();
    }
}
recsize=sizeof(emp);
while(1)
{
    printf("
1.Add Records
2.Delete Records
3.Modify Records
4.List Records
5.Exit");
    printf("Enter your choice");
    fflush(stdin);
    scanf("%c",&choice);
    switch(choice)
    {
        case'1':
            fseek(fp,0,SEEK_END);
            another='Y';
            while(another=='Y'||another=='y')
            {
                printf("Enter the first name,last name,age and basic salary : ");
                scanf("%s %s %d %f",emp.fname,&emp.age,&emp.bsal);
                printf(" Enter joining date,id,last education,subject taken");
                scanf("%s %s %d %s %s",emp.join_date,&emp.id,emp.last_edu,emp.sub_taken);
                fwrite(&emp,recsize,1,fp);
                printf(" Add another Record (Y/N): ");
```