```
```cpp
}
else
{
    return p->second;
}
}
```
```

```
```cpp
vector<string> TelephoneDirectory::find_entries(int number)
{
    multimap<int, string>::iterator lower
        = inverse_database.lower_bound(number);
    multimap<int, string>::iterator upper
        = inverse_database.upper_bound(number);
    vector<string> result;

    for (multimap<int, string>::iterator pos = lower;
         pos != upper; pos++)
    {
        result.push_back(pos->second);
    }
    return result;
}
```
```

```
```cpp
void TelephoneDirectory::print_all()
{
    for (map<string, int>::iterator pos = database.begin();
         pos != database.end(); pos++)
    {
        cout << pos->first << ": " << pos->second << endl;
    }
}
```
```

```
```cpp
int main()
{
    TelephoneDirectory data;
    data.add_entry("Fred", 7235591);
    data.add_entry("Mary", 3841212);
    data.add_entry("Sarah", 3841212);
    cout << "Number for Fred: " << data.find_entry("Fred") << endl;
    vector<string> names = data.find_entries(3841212);
    cout << "Names for 3841212: ";
    for (int i = 0; i < names.size(); i++)
    {
        cout << names[i] << " ";
    }
    cout << endl;
    cout << "All names and numbers:" << endl;
    data.print_all();
    return 0;
}
```
```

# Program Run

```
```text
Number for Fred: 7235591
Names for 3841212: Mary Sarah
All names and numbers:
Fred: 7235591
Mary: 3841212
Sarah: 3841212
```
```