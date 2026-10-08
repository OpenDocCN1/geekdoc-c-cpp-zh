# 17.3 Creating a Sequential-Access Text File 743

```
43 else // set array values if array has correct length
44 {
45     // set array values to TextBox values
46 accountTextBox.Text = values[(int] TextBoxIndices.Account];
47 firstNameTextBox.Text = values[(int] TextBoxIndices.First];
48 lastNameTextBox.Text = values[(int] TextBoxIndices.Last];
49 balanceTextBox.Text = values[(int] TextBoxIndices.Balance];
50 
51     }
52 
53 // return TextBoxValues as string array
54 public string[] GetTextBoxValues()
55 {
56     return new string[] {
57         accountTextBox.Text, firstNameTextBox.Text,
58         lastNameTextBox.Text, balanceTextBox.Text};
59     }
60 }
61 }
```

![](bbox=[0.347, 0.417, 0.652, 0.584])

Fig. 17.2 | A reusable Windows Form for the examples in this chapter. (Part 2 of 2.)

# Class Record

Figure 17.3 contains class Record that Figs. 17.4, 17.6 and 17.7 use for maintaining the information in each record's written to or read from a file. This class also belongs to the BankLibrary, so it's located in the same project as BankUIForm.

```
1 // Fig. 17.3: Record.cs
2 // Class that represents a data record.
3 namespace BankLibrary
4 {
5     public class Record
6 {
7         public int Account { get; set; }
8         public string FirstName { get; set; }
9         public string LastName { get; set; }
10        public decimal Balance { get; set; }
11    }
```

Fig. 17.3 | Class that represents a data record. (Part I of 2.)