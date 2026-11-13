```
void add_saleamt()
{
    int x;
    x = strcmp(city, "Delhi");
    if(x == 0)
    {
        Delhi_Sale = Delhi_Sale + sale_amt;
    }
    x = strcmp(city, "Nashik");
    if(x == 0)
    {
        Nashik_Sale = Nashik_Sale + sale_amt;
    }
    x = strcmp(city, "Cochin");
    if(x == 0)
    {
        Cochin_Sale = Cochin_Sale + sale_amt;
    }
    x = strcmp(city, "Akola");
    if(x == 0)
    {
        Akola_Sale = Akola_Sale + sale_amt;
    }
    Total_Sale_Amount = Akola_Sale + Cochin_Sale
    + Delhi_Sale + Nashik_Sale;
}
// static member function
static void display_saleamt()
{
    cout << "\n Total sale amount in Akola = " <<
    Akola_Sale;
    cout << "\n Total sale amount in Delhi = " <<
    Delhi_Sale;
    cout << "\n Total sale amount in Cochin = " <<
    Cochin_Sale;
    cout << "\n Total sale amount in Nashik = " <<
    Nashik_Sale;
    cout << "\n Total sale amount of a company in
all cities = ";
    cout << Total_Sale_Amount;
}
}; // end of class
//define static variables
int sale :: Delhi_Sale, Cochin_Sale, Akola_Sale,
Nashik_Sale;
int sale :: Total_Sale_Amount;
void main()
{
    ...
    sale :: display_saleamt();
} // end of main
```