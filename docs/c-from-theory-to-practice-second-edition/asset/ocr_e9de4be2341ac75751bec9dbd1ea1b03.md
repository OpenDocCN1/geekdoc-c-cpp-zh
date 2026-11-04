```
~~~cpp
catch(string msg)
{
    cout << msg;
}
catch(int code)
{
    if(code == 20)
        cout << "Error: " << name << " contains number\n";
    else if(code == 30)
        cout << "Error: " << name << " contains sign\n";
}
catch(...) /* We added this block, just to see it. */
{
    cout << "Error: Another exception\n";
}
return 0;

void check_grd(float grd)
{
    string msg;

    if(grd > 10)
        throw grd;
    else if(grd < 0)
    {
        msg = "Error: negative number is entered\n";
        throw msg;
    }
}

void check_name(string n)
{
    for(int i = 0; i < n.length(); i++)
    {
        if(n[i] >= '0' && n[i] <= '9')
            throw 20;
        else if(n[i] == '+' || n[i] == '-')
            throw 30;
    }
}
~~~
```

Well, how did you like this quick tour? Hope we didn't tire you. You've got a C++ feeling, go on to next chapter to visit planet Java.