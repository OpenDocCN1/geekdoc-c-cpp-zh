```
void tally() { count++; }

bool operator==(const AddressCounter & addr2)
{ return address == addr2.address; }

string getAddress() const
{ return address; }

private:
    string address;
    int count;
};
//---------------- End class AddressCounter ---------------------

typedef list<AddressCounter> IP_List;

int main()
{
    string fileName;                     // file of IP addresses
    IP_List addrCountList;               // list of addresses

    ifstream inStream;                   // open file of addresses
    cout << "Enter name of file containing IP addresses: ";
    cin >> fileName;
    inStream.open(fileName.data());
    assert(inStream.is_open());

    AddressCounter item;                 // one address & its count
    for (;;)                             // input loop:
    {
        item.read(inStream);             //   read an address
        if (inStream.eof()) break;       //   if eof, quit

        IP_List::iterator it =           //   is item in list?
            find(addrCountList.begin(), addrCountList.end(), item);
        if (it != addrCountList.end())   //   if so:
            (*it).tally();               //       ++ its count
        else                             //   otherwise
            addrCountList.push_back(item); //       add it to the list
    }                                    //   end loop

    cout << "\nAddresses and Counts:\n\n";  // output the list
    for (IP_List::iterator it = addrCountList.begin();
                         it != addrCountList.end(); it++)
        (*it).print(cout);
}
```

# LISTING OF FILE ipAddresses.txt USED IN SAMPLE RUN:

128.159.4.20