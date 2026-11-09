
## GET RID OF THOSE SPACES

When entering data in a text box or input box, it's not unusual for a user to inadvertently press the spacebar after typing the data, thereby including an extraneous space character at the end of the data. You can use the **Trim method** to remove (trim) any spaces from both the beginning and end of a string. Figure 24-2 shows the method's syntax and includes an example of using the method. When processing the Trim method, the computer first makes a temporary copy of the *string* in memory. It then performs the necessary trimming on the copy only. In other words, the Trim method does not remove any characters from the original *string*. The Trim method returns a string that excludes any leading or trailing spaces.

### USING THE TRIM METHOD

| Syntax | Purpose |
| --- | --- |
| *string.Trim* | removes any spaces from both the beginning and end of a string |

**Example**

`strFullName = txtName.Text.Trim`

assigns the contents of the txtName control, excluding any leading and trailing spaces, to the strFullName variable

**Figure 24-2:** Syntax and an example of the Trim method

You will use both the Length property and the Trim method in the Product ID application, which you code in the next section.

## THE PRODUCT ID APPLICATION

The Product ID application displays (in a label control) a listing of the product IDs entered by the user. Each product ID must contain exactly five characters.

**To open the Product ID application, and then code and test the application:**

- 1. Start Visual Studio 2008 (or Visual Basic 2008 Express Edition). Open the **Product Solution (Product Solution.sln)** file, which is contained in the ClearlyVB\Chap24\Product Solution folder. If necessary, open the designer window. The user interface provides a text box for entering the product ID.
- 2. Open the Code Editor window, then locate the code template for the btnAdd control's Click event procedure. Before verifying the product ID's length, you will remove any leading and trailing spaces from the ID. Click the **blank line** below the 'remove any leading and trailing spaces' comment. Type `strId = txtId.Text.Trim` and press **Enter**.
- 3. Now determine whether the ID contains exactly five characters. Click the **blank line** below the 'verify length' comment. Type `If strId.Length = 5 Then` and press **Enter**.
- 4. If the ID contains exactly five characters, the procedure should display the ID in the lblListing control; otherwise, it should display an appropriate message. Type the lines of code indicated in Figure 24-3.

```vb
Private Sub btnAdd_Click(ByVal sender As Object, ByVal e As System.EventArgs)
    ' add product ID to listing

    Dim strId As String

    ' remove any leading and trailing spaces
    strId = txtId.Text.Trim

    ' verify length
    If strId.Length = 5 Then
        lblListing.Text = lblListing.Text & strId.ToUpper _
            & ControlChars.NewLine
    Else
        MessageBox.Show("The product ID must contain 5 characters.", _
            "Product ID", MessageBoxButtons.OK, _
            MessageBoxIcon.Information)
    End If

    txtId.Focus()
End Sub
```

enter these six lines of code

**Figure 24-3:** Completed Click event procedure for the btnAdd control

- 5. Save the solution, then start the application. First, enter an ID that contains four characters. Type **abc2** as the product ID, then click the **Add to List** button. A message box opens and displays the message “The product ID must contain 5 characters.” Close the message box.
- 6. Now include two trailing spaces after the ID. Change the product ID to **abc23**, then press the **Spacebar** twice. Click the **Add to List** button. ABC23 appears in the listing of product IDs.
- 7. On your own, test the application using an ID that contains nine characters. Also test it using an ID that contains both leading and trailing spaces. When you are finished testing the application, click the **Exit** button. Close the Code Editor window, then close the solution.

## LET'S MAKE A SUBSTITUTION

Visual Basic provides the **Replace method** for replacing a sequence of characters in a string with another sequence of characters, such as replacing area code “(800)” with area code “(877)” in a phone number. Figure 24-4 shows the syntax of the Replace method and includes examples of using the method. In the syntax, *oldValue* is the sequence of characters that you want to replace in the *string*, and *newValue* is the replacement characters. When processing the Replace method, the computer makes a temporary copy of the *string* in memory, and then replaces the characters in the copy only. The Replace method returns a string with *all* occurrences of *oldValue* replaced with *newValue*.

### USING THE REPLACE METHOD

| Syntax | Purpose |
|---|---|
| `string.Replace(oldValue, newValue)` | replaces every occurrence of *oldValue* with *newValue* |

**Example 1**

```vb
strPhone = "(800) 111-2222"
strPhone = strPhone.Replace("(800)", "(877)")
```

assigns the string "(877) 111-2222" to the strPhone variable

**Example 2**

```vb
strWord = "latter"
strWord = strWord.Replace("t", "d")
```

assigns the string "ladder" to the strWord variable

**Figure 24-4:** Syntax and examples of the Replace method

## I NEED TO FIT THIS IN SOMEWHERE

Rather than replacing characters in a string, an application may need to insert characters in a string. You insert characters using the **Insert method**. Possible uses for the method include inserting an employee’s middle initial within his or her name, or inserting parentheses around the area code in a phone number. Figure 24-5 shows the Insert method’s syntax. In the syntax, *startIndex* specifies where in the *string* you want the *value* inserted. The *startIndex* argument is an integer that represents the character’s index—in other words, its position in the string. The first character in a string has an index of 0, the second character an index of 1, and so on. To insert the *value* beginning with the fifth character in the string, you use a *startIndex* of 4, as shown in the example in Figure 24-5. When processing the Insert method, the computer makes a temporary copy of the *string* in memory, and then inserts the characters in the copy only. The Insert method returns a string with the appropriate characters inserted.

### USING THE INSERT METHOD

| Syntax | Purpose |
|---|---|
| `string.Insert(startIndex, value)` | inserts characters in a string |

**Example**

```vb
strName = "Rob Smith"
strFullName = strName.Insert(4, "T. ")
```

assigns the string “Rob T. Smith” to the strFullName variable

**Figure 24-5:** Syntax and an example of the Insert method

You will use the Replace and Insert methods in the Phone Numbers application, which you code in the next section.

## THE PHONE NUMBERS APPLICATION

The Phone Numbers application saves (in a sequential access file) the phone numbers entered by the user. Each phone number is entered using 12 characters in the following format: 111-222-3333. Before writing a phone number to the file, the application removes the hyphens and then verifies that the phone number contains 10 characters (the original 12 characters minus the two hyphens). The application also displays the phone numbers contained in the file, both with and without the hyphens.

**To open the Phone Numbers application, and then begin coding the application:**

- 1. Open the **Phone Solution (Phone Solution.sln)** file, which is contained in the *ClearlyVB\Chap24\Phone Solution* folder. If necessary, open the designer window. The user interface provides a text box for entering the phone number.
- 2. Open the Code Editor window, then locate the code template for the btnSave control's Click event procedure. Before saving the phone number to the sequential access file, the procedure will replace the hyphens with the empty string. Click the **blank line** below the 'remove the hyphens' comment. Type **`strPhone = txtPhone.Text.Replace("-", String.Empty)`** and press **Enter**.
- 3. Save the solution, then start the application. First, enter an invalid phone number. Type **111-2222** as the phone number, then click the **Save** button. A message box opens and displays the “Invalid phone number” message. Close the message box.
- 4. Type **111-222-3333** as the phone number, then click the **Save** button. Type **222-333-4444** as the phone number, then click the **Save** button. Click the **Display** button. The button's Click event procedure reads each phone number from the phoneNumbers.txt file and displays each in the lblFileContents control. See Figure 24-6. Notice that the phone numbers do not contain any hyphens.

![](img/cf88270932e011575089da06b940a1d9_558_0.png)

**Figure 24-6:** Contents of the phoneNumbers.txt file displayed in the lblFileContents control

- 5. Click the **Exit** button.

In addition to displaying the phone numbers contained in the file, the Display button also should insert the appropriate hyphens in each number and then display the formatted number in the lblFormattedNumbers control. You can insert the hyphens using the Insert method, as shown in Figure 24-7.
