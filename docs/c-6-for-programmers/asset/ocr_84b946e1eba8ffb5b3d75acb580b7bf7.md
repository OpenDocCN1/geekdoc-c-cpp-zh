uses an object-creation expression

```
new Account()
```

to create an Account object, then assigns it to the variable myAccount. The variable's type is Account—the class we'll define in Fig. 4.2. Keyword new creates a new object of the specified class—in this case, Account. The parentheses to the right of Account are required (we'll discuss these in Section 4.8).

# 4.2.2 Calling Class Account's GetName Method

The Account class's GetName method returns the account name stored in a particular Account object. Line 13 of Fig. 4.1

```
Console.WriteLine($"Initial name is: {myAccount.GetName()}");
```

displays myAccount's initial name by calling the object's GetName method with the expression myAccount.GetName(). To call this method for a specific object, you specify

+   - the object's name (myAccount) followed by
+   - the member access operator (.), and
+   - the method name (GetName) and
+   - a set of parentheses.

The empty parentheses indicate that GetName does not require any additional information to perform its task. Soon, you'll see the SetName method that does require additional information to perform its task.

When Main calls the GetName method:

+   1. The app transfers execution from the expression myAccount.GetName() (line 13 in Main) to method GetName's declaration (which we'll study in Section 4.3). Because GetName was accessed via the object myAccount, GetName knows which object's data to manipulate.
+   2. Next, method GetName performs its task—that is, it returns the myAccount object's name to line 13 where the method was called.
+   3. Console.WriteLine displays the string returned by GetName—the name is inserted into the interpolated string in place of the call to GetName—then the program continues executing at line 16 in Main.

Because we have not yet stored a name in the myAccount object, line 13 does not display a name.

# 4.2.3 Inputting a Name from the User

Next, lines 16–17 prompt for and input a name. Line 17

```
string theName = Console.ReadLine(); // read a line of text
```