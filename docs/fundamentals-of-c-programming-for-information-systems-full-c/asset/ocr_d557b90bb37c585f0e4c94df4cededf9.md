`ArrayName` is the name of a one-dimensional array, and `SearchValue` is the value you are trying to find in an array. The method returns the index of the first element that matches the specified value. If no value is found, the method returns -1.

For example,

```csharp
Array.IndexOf(names, “Mike Burns”)
```

returns the index of the first element of the names array that matches the specified value, Mike Burns.

Figure 8-14 shows the code that uses this method to find a vendor’s phone number by searching for a specified name.

# **Figure 8-14:** Code to find the phone number using IndexOf method

```
private void btnFindPhone_Click(object sender, EventArgs e)
{
    string searchName = txtVendorName.Text;
    string fmtStr = "{0,-15}{1,8}";
    lstDisplay.Items.Clear();

    // Method 1: Use IndexOf method to find the record
    int index = Array.IndexOf(names, searchName);
        //if there is no match, index would be -1.
    if (index >= 0)
        lstDisplay.Items.Add(string.Format(fmtStr, searchName,
                                           phoneNumbers[index]));
    else
        MessageBox.Show("Sorry, name not found");
}
```

**Line 60** uses the IndexOf method to get the index of the element in the Names array that matches the value of SearchName.

**Lines 62–64** display the corresponding element from phoneNumbers array if the index is not -1. If not, a message is displayed.

Figure 8-15 shows an alternate method that uses a loop to compare the value of SearchName with each element in the Names array.

# **Figure 8-15:** Using a loop to search a field

```
// Method 2: Use for loop to find the record
for (index = 0; index < recordCount; index++)
{
    if (searchName == names[index])
    {
        lstDisplay.Items.Add(String.Format(fmtStr, names[index],
                                            phoneNumbers[index]));
        return;
    }
}
MessageBox.Show("Sorry, there is no Vendor by that name");
```