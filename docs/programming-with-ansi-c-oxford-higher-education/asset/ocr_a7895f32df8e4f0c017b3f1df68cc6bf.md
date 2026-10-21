```
class customer
{
    int CustId;
    string Name;

public:
    customer()
    {
        CustId = 0;
        Name = "Dummy";
    }

    customer(int TempCustId, string TempName)
    {
        CustId = TempCustId;
        Name = TempName;
    }

    friend ostream & operator <<(ostream & TempOut, customer TempCustomer);
};

ostream & operator <<(ostream & TempOut, customer TempCustomer)
{
    TempOut << TempCustomer.CustId << " " << TempCustomer.Name << endl;
    return TempOut;
}

int main()
{
    fstream CustomerFile("Customers.dat", ios::in | ios::out | ios::trunc| ios::binary);

    customer Lara(1, "Brian Charles Lara");
    customer Beckham(2, "David Beckham");
    customer Steffi(3, "Steffi Graf");
    customer Answer1, Answer2;
    CustomerFile.write((char *) &Lara, sizeof(Lara));
    CustomerFile.write((char *) &Beckham, sizeof(Beckham));
    CustomerFile.write((char *) &Steffi, sizeof(customer));

    cout << "Initial stage \n";
    cout << "The get pointer is at byte no. " << CustomerFile.tellg() << endl;
    cout << "The put pointer is at byte no. " << CustomerFile.tellp() << endl;

    CustomerFile.seekg(0, ios::beg);
    cout << "After seekg() is moved to the beginning of the file \n";

    cout << "The get pointer is at byte no. " << CustomerFile.tellg() << endl;
    cout << "The put pointer is at byte no. " << CustomerFile.tellp() << endl;
    cout << "Record no. 1 is as follows \n";

    if(!CustomerFile.read((char *) &Answer1, sizeof(customer)))
    cout << "Error in reading file";
    cout << Answer1;

    cout << "Record no. 3 is as follows \n";
    CustomerFile.seekg(2 * sizeof(customer), ios::beg);

    cout << "After seekg() is moved to the end of the second record \n";

    cout << "The get pointer is at byte no. " << CustomerFile.tellg() << endl;
    cout << "The put pointer is at byte no. " << CustomerFile.tellp() << endl;
    CustomerFile.read((char *) &Answer2, sizeof(customer));
    cout << Answer2;
```