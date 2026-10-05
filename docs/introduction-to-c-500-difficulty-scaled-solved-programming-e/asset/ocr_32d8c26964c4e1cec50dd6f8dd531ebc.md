```
check_pswd(pswd);
    break;
}
catch(const Err_Rpt& err)
{
    err.show();
}
catch(int code)
{
    cout << "C:" << code << ' << "Error: Password must contain one special character at least\n";
}
catch(...)
{
    cout << "Error: Another exception\n";
}
cout << "Password " << pswd << " is accepted !!!\n";
return 0;

```

```
int check_pswd(const string& str)
{
    bool found;
    int i, len;

    len = str.size();
    if(len < 6)
        throw Err_Rpt(5, "Error: Short length\n"); /* Create an exception with type object of the Err_Rpt class. */
    int dig = 0;
    found = false;
    for(i=0; i<len; i++)
    {
        if(str[i] >= '0' && str[i] <= '9')
            dig++;
        if(str[i] == '!' || str[i] == '$' || str[i] == '#')
            found = true;
    }
    if(dig < 3)
        throw Err_Rpt(10, "Error: Password must contain three digits at least\n");
    if(found == false)
        throw 20;
    return 0;

```

First, I changed the code so that the user enters a valid password, the break statement terminates the loop and displays it. The continue statements are unnecessary since no code exists after the last catch block. The check_pswd() throws an exception with type int and two other types with Err_Rpt object. Each object is initialized with values that indicate the type of error. These exceptions are caught by the respective catch block, which calls the show() of the passed object to display the information contained in members.

Note that instead of the int exception we could throw another exception of Err_Rpt type. For example, we can write throw Err_Rpt(); where the passed object does not contain any information.