# ## 5.4 Protecting Passwords

When using SQL pass-through statements to access remote databases we often have to pass user identification and password information to the remote database. If we use those passwords in our program, our user ID and password will be surfaced for all to see. Very often we need to protect our passwords and to a lesser extent our user ID. The level of protection will vary from industry to industry, but the basics are the same.

Fortunately there are a number of ways to protect our passwords.

# ### 5.4.1 Using PROC PWENCODE

The PWENCODE procedure can be used to encode or encrypt passwords. *Encoding* is a text substitution technique that disguises your password through a series of text substitutions. *Encryption*, which is a more secure method than encoding (available starting in SAS 9.2), uses mathematical operations in the transformation of the text.

I have had very limited success at using this procedure to protect passwords. First, encoding is not a very strong protection, but more importantly the encoded or encrypted text can often be used instead of the password. It does not particularly matter if the bad guys cannot ‘see’ the actual password if the encoded text string, which they can see, will work in its place.

Encoding or encrypting your password through PROC PWENCODE creates and then allows you to use a text string instead of the actual password. It protects your password from being viewed directly, since only the encoded/encrypted string is visible. However, remember that the visible string, while not the password, can still be used as the password. This means that we will also need to protect this encoded/encrypted string.

```
```sas
filename pwfile "path\\results\\pwfile.txt";
proc pwencode in="pharmer" out=pwfile;
  run;
```
```

In this PWENCODE step our password ‘pharmer’ is to be encrypted (under SAS 9.1 the default was encoding). As the procedure executes, the encrypted value of ‘pharmer’ is written to the text file (PWFILE.TXT) as: `{sas002}81F6943F251507393B969C0753B2D73B` and is not otherwise surfaced for viewing.

Once the value has been stored in the text file, it can be recovered and used at some point in the future. The SAS documentation for PROC PWENCODE shows how this value can be stored in a macro variable or written to the LOG. Both approaches are not practical, because if the user (or someone else) can see the encoded/encrypted value, they can then use it instead of the real password. They may not know your real password, but that does not matter; they still have access to your data.

We need to be able to use the password without ever surfacing its value, either in a macro variable or to the LOG. The following DATA step the LIBNAME function is used to create a *libref* which establishes an ODBC connection to an SQL server. The password is recovered from the text file and the value is inserted into the PASSWORD= option.