```
```csharp
// enable all GUI buttons, except for Open File button
openButton.Enabled = false;
creditButton.Enabled = true;
debitButton.Enabled = true;
zeroButton.Enabled = true;
}
}
}

// invoked when user clicks credit balances,
// debit balances or zero balances button
private void getBalances_Click(object sender, System.EventArgs e)
{
    // convert sender explicitly to object of type Button
    Button senderButton = (Button) sender;

    // get text from clicked button, which stores account type
    string accountType = senderButton.Text;

    // read and display file information
    try
    {
        // go back to the beginning of the file
        input.Seek(0, SeekOrigin.Begin);

        displayTextBox.Text =
            $"Account with {accountType}{Environment.NewLine}";

        // traverse file until end of file
        while (true)
        {
            // get next Record available in file
            string inputRecord = fileReader.ReadLine();

            // when at the end of file, exit method
            if (inputRecord == null)
            {
                return;
            }

            // parse input
            string[] inputFields = inputRecord.Split(',');

            // create Record from input
            var record =
                new Record(int.Parse(inputFields[0]), inputFields[1],
                    inputFields[2], decimal.Parse(inputFields[3]));

            // determine whether to display balance
            if (ShouldDisplay(record.Balance, accountType))
            {
```
```

*Fig. 17.7* | Credit-inquiry program. (Part 2 of 5.)