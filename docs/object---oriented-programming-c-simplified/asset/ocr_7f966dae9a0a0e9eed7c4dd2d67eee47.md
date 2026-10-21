```
{
    r = save%10;
    rev = rev*10 + r;
    save = save/10;
}
if(rev == num)
    return 1;
else
    return 0;
}
void main()
{
    Palin obj;
    int x;
    clrscr();
    cout << "Enter the number to be checked for palindrome\n";
    cin >> x;
    obj.input(x);
    if(obj.checkpalin() == 1)
        cout << obj.getnum() << "is palindrome\n";
    else
        cout << obj.getnum() << "is not palindrome\n";
    getch();
}
```

# OUTPUT :

(FIRST RUN)

Enter the number to be checked for palindrome

4554

4554is palindrome

(SECOND RUN)

Enter the number to be checked for palindrome

4567

4567is not palindrome

# EXPLANATION :

A number is called palindrome if on reversing it is equal to the original number for e.g., 121,3223, 656 etc. To check whether an enetered number is palindrome or not simply reverse the number and compare with the original number but as we have seen in the