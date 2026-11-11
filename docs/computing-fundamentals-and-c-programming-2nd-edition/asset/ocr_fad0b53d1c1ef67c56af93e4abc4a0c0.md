```
```c
}
break;

/* To login an employee into the system and record the login date and time*/
case 5:
    clrscr();
    gotoxy(20,4);
    printf("DAILY EMPLOYEE TIME RECORDING SYSTEM");
    gotoxy(20,23);
    printf("Warning: Please Enter Numeric Values Only.");
    gotoxy(23,7);
    printf("Enter Your Id to Login: ");
    scanf("%d", &searchid);
    gotoxy(20,23);
    printf("                                 ");
    findEmployee='f';
    rewind(db);
        while((fread(&empData,size,1,db))==1)
    {
        if (empData.empid==searchid)
        {
        gotoxy(23,8);
        printf("Enter Your Password: ");

            for (i=0;i<6;i++)
            {
                pass[i]=getch();
                printf("* ");
            }
            pass[6]='\0';
        while(getch()!=13);

        if (strcmp(empData.password,pass))
        {
            gotoxy(23,11);
            textcolor(YELLOW+BLINK);
            cprintf("You Have Supplied a Wrong Password.");
            textcolor(YELLOW);
            findEmployee='t';
            getch();
```
```