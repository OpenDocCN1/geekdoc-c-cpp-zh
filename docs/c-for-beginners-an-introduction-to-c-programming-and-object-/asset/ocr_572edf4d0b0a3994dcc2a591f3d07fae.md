```
        << "First Name: " << FirstName << endl
        << "Last Name: " << LastName << endl
        << "City: " << City << endl
        << "School: " << School << endl
        << "Grade: " << Grade << endl;
}

main ()
{
    Student s1, s2;

    s1.setData ("Roger", "Dimitri", "New York",
                , );
    s2.setData ("Claire", "Smith", "Los Angeles",
                , );

    s1.displayData ();
    s2.displayData ();
    cout << endl << endl;
    return ;
}
```

Output:

![](bbox=[0.1, 0.46, 0.97, 0.785])

Just like public data members can be inherited, public member functions can also be inherited. Let us modify the *Person* class as follows: