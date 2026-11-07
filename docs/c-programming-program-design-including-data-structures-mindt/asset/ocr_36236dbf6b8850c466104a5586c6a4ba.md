```
```cpp
//process the requests
while (choice != 9)
{
    switch (choice)
    {
    case 1:
        cout << "Enter the title: ";
        getline(cin, title);
        cout << endl;

        if (dvdList.dvdSearch(title))
            cout << "The store carries " << title
                 << endl;
        else
            cout << "The store does not carry "
                 << title << endl;
        break;

    case 2:
        cout << "Enter the title: ";
        getline(cin, title);
        cout << endl;

        if (dvdList.dvdSearch(title))
        {
            if (dvdList.isDVDAvailable(title))
            {
                dvdList.dvdCheckOut(title);
                cout << "Enjoy your movie: "
                     << title << endl;
            }
            else
                cout << "Currently " << title
                     << " is out of stock." << endl;
        }
        else
            cout << "The store does not carry "
                 << title << endl;
        break;

    case 3:
        cout << "Enter the title: ";
        getline(cin, title);
        cout << endl;

        if (dvdList.dvdSearch(title))
        {
            dvdList.dvdCheckIn(title);
            cout << "Thanks for returning "
                 << title << endl;
        }
```
```