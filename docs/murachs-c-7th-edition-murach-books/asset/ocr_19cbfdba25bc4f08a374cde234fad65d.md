# Code that parses a first name from a name string

```
string fullName = " Edward C Koop  ";    // " Edward C Koop  "
fullName = fullName.Trim();                // "Edward C Koop"
int firstSpace = fullName.IndexOf(" ");   // 6
string firstName = "";
if (firstSpace == -1)
    firstName = fullName;
else
    firstName = fullName.Substring(0, firstSpace);    // Edward
```

# Code that parses a string that contains an address

```
string address = " |805 Main Street|Dallas|TX|12345| ";
address = address.Trim();
if (address.StartsWith("|"))
    address = address.Remove(0, 1);
if (address.EndsWith("|"))
    address = address.Remove(address.Length - 1, 1);
int cityIndex = address.IndexOf("|") + 1;
int stateIndex = address.IndexOf("|", cityIndex) + 1;
int zipIndex = address.IndexOf("|", stateIndex) + 1;
string street = address.Substring(0, cityIndex - 1);
string city = address.Substring(cityIndex, stateIndex - cityIndex - 1);
string state = address.Substring(stateIndex, zipIndex - stateIndex - 1);
string zipCode = address.Substring(zipIndex);
```

# Code that uses the Split() method to parse the name string

```
string fullName = " Edward C Koop  ";
fullName = fullName.Trim();
string[] names = fullName.Split(' ');
string firstName = names[0];    // Edward
```

# Code that uses the Split() method to parse the address string

```
address = address.Trim();
if (address.StartsWith("|"))
    address = address.Remove(0, 1);
string[] columns = address.Split('|');
string street = columns[0];    // 805 Main Street
string city = columns[1];      // Dallas
string state = columns[2];     // TX
string zipCode = columns[3];   // 12345
```

# Code that adds hyphens to a phone number

```
string phoneNumber = "9775551212";
phoneNumber = phoneNumber.Insert(3, "-");
phoneNumber = phoneNumber.Insert(7, "-");    // 977-555-1212
```

# Code that replaces the hyphens in a date with slashes

```
string date = "12-27-2018";
date = date.Replace("-", "/");    // 12/27/2018
```