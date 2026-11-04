To verify that an email address is correctly formatted, you can use the following statements with the specified regular expression:

```
string email = "weimenglee@learn2develop.net";
Regex r = new Regex(@"^[\w\.-]+@[\w-]+\.[\w-]{2,4}$");
if (r.IsMatch(email))
    Console.WriteLine("Email address is correct.");
else
    Console.WriteLine("Email address is incorrect.");
```

There are many different regular expressions that you can use to validate an email address. However, there is no perfect regular expression to validate all email addresses. For more information on validating email addresses using regular expressions, check out the following web sites: http://regular-expressions.info/email.html and http://fightingforalostcause.net/misc/2006/compare-email-regex.php.

# Summary

String manipulations are common operations, so it’s important that you have a good understanding of how they work and the various methods and classes that deal with them. This chapter provided a lot of information about how strings are represented in C# and about using regular expressions to perform matching on strings.