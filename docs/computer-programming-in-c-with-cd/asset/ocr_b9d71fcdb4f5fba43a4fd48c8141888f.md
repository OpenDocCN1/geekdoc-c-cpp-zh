```
```cpp
break;

case 2:
    r.getStaff();
    r.getSalesPerson();
    r.getRegular();
    r.displayStaff();
    r.displaySalesPerson();
    r.displayRegular();
    break;

case 3:
    c.getStaff();
    c.getSalesPerson();
    c.getCasual();
    c.displayStaff();
    c.displaySalesPerson();
    c.displayCasual();
    break;

case 4:
    o.getStaff();
    o.getOfficer();
    o.displayStaff();
    o.displayOfficer();
    break;
    default:cout<<"Not a right choice..."<<endl;
}
cout<<"Do you want to continue (Y for yes and N for
No)?"<<endl;
cin>>choice;
}while(choice=='y'||choice=='Y');
}

Output:

Employee Details
1 : Typist
2 : Sales Person (Regular)
3 : Sales Person (Casual)
4 : Officer
1
Enter name : Meena

Enter code : 101

Enter speed (no. of words per minute): 60

Enter experience (no. of years) : 1
```
```