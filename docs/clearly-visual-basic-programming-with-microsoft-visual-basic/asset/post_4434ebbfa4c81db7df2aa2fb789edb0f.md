
### Example 3

```vb
    Do While strId Like "###"
```

The condition evaluates to True when the string stored in the strId variable begins with three digits followed by zero or more characters; otherwise, it evaluates to False. Examples of *strings* that would make the condition evaluate to True include "178" and "983Ab". Examples of *strings* for which the condition would evaluate to False include "X34" and "34Z5".

### Example 4

```vb
    If strFirstName.ToUpper Like "T[OI]M" Then
```

The condition evaluates to True when the string stored in the strFirstName variable (converted to uppercase) is either "TOM" or "TIM". When the strFirstName variable does not contain "TOM" or "TIM"—for example, when it contains "TAM" or "Tommy"—the condition evaluates to False.

### Example 5

```vb
    If strLetter Like "[a-z]" Then
```

The condition evaluates to True when the string stored in the strLetter variable is a lowercase letter; otherwise, it evaluates to False.

### Example 6

```vb
    For intIndex As Integer = 0 To strUserEntry.Length - 1
        If strUserEntry.Substring(intIndex, 1) Like "[!a-zA-Z]" Then
            intNonLetter = intNonLetter + 1
        End If
    Next intIndex
```

Compares each character contained in the strUserEntry variable with the lowercase and uppercase letters of the alphabet, and counts the number of characters that are not letters.

**Figure 24-14:** *Syntax and examples of the Like operator (continued from previous page)*

## MODIFYING THE PRODUCT ID APPLICATION

Earlier in the chapter, you coded the Product ID application, which displayed a listing of the product IDs entered by the user. As you may remember, each product ID contained exactly five characters. In the following set of steps, you will modify the application to ensure that the five characters are three letters followed by two numbers.

![](img/cf88270932e011575089da06b940a1d9_567_0.png)

Before completing the next set of steps, it may be helpful to view the Ch24-Like operator video.

To modify the Product ID application, and then test the application:

- 1. Use Windows to make a copy of the Product Solution folder. Save the copy in the ClearlyVB\Chap24 folder. Rename the copy Modified Product Solution.
- 2. Open the **Product Solution (Product Solution.sln)** file contained in the ClearlyVB\Chap24\Modified Product Solution folder. Open the designer window.
- 3. Open the Code Editor window and locate the btnAdd control's Click event procedure. Change the 'remove any leading and trailing spaces' comment to '**remove any leading and trailing spaces, then convert to uppercase.**' Also change the strId = txtId.Text.Trim statement to **strId = txtId.Text.Trim.ToUpper.**
- 4. Change the 'verify length' comment to '**verify that the ID contains 3 letters followed by 2 numbers.**' Also change the If clause to **If strId Like "[A-Z][A-Z][A-Z]##" Then**.
- 5. In the statement below the If clause, change strId.ToUpper to **strId**. Finally, change the message in the MessageBox.Show method to **"Invalid product ID"**. Figure 24-15 shows the modified Click event procedure. The modified comments and code are shaded in the figure.

```vb
Private Sub btnAdd_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles btnAdd.Click
    ' add product ID to listing

    Dim strId As String

    ' remove any leading and trailing spaces, then convert to uppercase
    strId = txtId.Text.Trim.ToUpper

    ' verify that the ID contains 3 letters followed by 2 numbers
    If strId Like "[A-Z][A-Z][A-Z]##" Then
        lblListing.Text = lblListing.Text & strId _
            & ControlChars.NewLine
    Else
        MessageBox.Show("Invalid product ID", _
            "Product ID", MessageBoxButtons.OK, _
            MessageBoxIcon.Information)
    End If

    txtId.Focus()
End Sub
```

Figure 24-15: Modified comments and code

- 4. If the strMessage variable contains the string "Today is Monday", which of the following assigns the number 9 to the intNum variable?
  - a. intNum = strMessage.Substring("M")
  - b. intNum = strMessage.Substring("M", 1)
  - c. intNum = strMessage.IndexOf("M")
  - d. intNum = strMessage.IndexOf(0, "M")

- 5. If the strName variable contains the string "John Jones", which of the following changes the contents of the variable to "John K. Jones"?
  - a. strName = strName.Replace(" ", " K. ")
  - b. strName = strName.Insert(5, "K. ")
  - c. strName = strName.Insert(4, " K.")
  - d. All of the above.

## EXERCISES

- 1. **TRY THIS** The strAmount variable contains the string "3,123,560". Write the Visual Basic statement to change the contents of the variable to "3123560"; use the Replace method. Now that the strAmount variable contains the string "3123560", write the Visual Basic statements to change the variable's contents to "$3,123,560". (The answers to TRY THIS Exercises are located at the end of the chapter.)

- 2. **TRY THIS** Open the Zip Solution (Zip Solution.sln) file, which is contained in the ClearlyVB\Chap24\Zip Solution folder. Open the designer window. The Display Shipping Charge button's Click event procedure should display the appropriate shipping charge based on the ZIP code entered by user. To be valid, the ZIP code must contain exactly five digits, and the first three digits must be either "605" or "606". The shipping charge for "605" ZIP codes is $25. The shipping charge for "606" ZIP codes is $30. Display an appropriate message if the ZIP code is invalid. Code the procedure. Save the solution, then start the application. Test the application using the following ZIP codes: 60677, 60511, 60344, and 7130. Stop the application, then close the solution. (The answers to TRY THIS Exercises are located at the end of the chapter.)

- 3. **MODIFY THIS** In this exercise, you modify the Phone Numbers application coded in the chapter. Use Windows to make a copy of the Phone Solution folder. Save the copy in the ClearlyVB\Chap24 folder. Rename the copy Phone Solution-MODIFY THIS. Open the Phone Solution (Phone Solution.sln) file, which is contained in the ClearlyVB\Chap24\Phone Solution-MODIFY THIS folder. Open the designer window. The btnSave control's Click event procedure should determine whether the user entered the phone number in the required format: three digits, a hyphen, three digits, a hyphen, and four digits. Display an appropriate message if the format is not correct. Modify the procedure appropriately. Save the solution, then start the application. Test the application using the following phone numbers: 1-234-567890 and 999-888-1111. Stop the application, then close the solution.

- 4. **INTRODUCTORY** Open the CityState Solution (CityState Solution.sln) file, which is contained in the ClearlyVB\Chap24\CityState Solution folder. Open the designer window. The interface provides a text box for entering the name of a city, followed by a comma, a space, and a state name. The Display Message button's Click event procedure should display the message "cityName is located in stateName", where cityName and stateName are the names of the city and state entered by the user. Code the procedure. Save the solution, then start and test the application. Stop the application, then close the solution.

- 5. **INTERMEDIATE** Open the Color Solution (Color Solution.sln) file, which is contained in the ClearlyVB\Chap24\Color Solution folder. Open the designer window. The Display Color button's Click event procedure should display the color of the item whose item number is entered by the user. All item numbers contain exactly five characters. All items are available in four colors: blue, green, red, and white. The third character in the item number indicates the item's color, as follows: a B or b indicates Blue, a G or g indicates Green, an R or r indicates Red, and a W or w indicates White. The procedure should display an appropriate message when the item number does not contain exactly five characters, or when the third character is not one of the valid color characters. Save the solution, then start the application. Test the application using 12b45 as the item number. The procedure should display the word "Blue" in the lblColor control. Test the application using the following valid item numbers: 99G44, abr55, and 78w99. Now test the application using the following invalid item numbers: 12x and 23abc. Stop the application, then close the solution.

- 6. **ADVANCED** Open the Jacobson Solution (Jacobson Solution.sln) file, which is contained in the ClearlyVB\Chap24\Jacobson Solution folder. Open the designer window. The interface provides a text box for entering a password. The text box's CharacterCasing property is set to Upper. The password can contain 5, 6, or 7 characters, but no space characters. The Display New Password button should create and display a new password using the following three rules. First, replace all vowels (A, E, I, O, and U) with the letter X. Second, replace all numbers with the letter Z. Third, reverse the characters in the password. Save the solution, then start and test the application. Stop the application, then close the solution.

- 7. Open the FigureThisOut Solution (FigureThisOut Solution.sln) file, which is contained in the ClearlyVB\Chap24\FigureThisOut Solution folder. Open the Code Editor window and study the existing code. What task is performed by the btnDisplay control's Click event procedure? Start and then test the application. Stop the application. Close the Code Editor window, then close the solution.

![](img/cf88270932e011575089da06b940a1d9_571_0.png)
