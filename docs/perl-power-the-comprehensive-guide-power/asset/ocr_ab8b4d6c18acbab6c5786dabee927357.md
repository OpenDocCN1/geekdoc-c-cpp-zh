# # CHAPTER 15 Regular Expressions

```
s/b/ben/;
}
#Change the lowercase to the uppercase for the range
foreach(@AlphaNumSet){
    $_ =~ tr/[a-b]/[A-B]/;
}
```

The results of the substitution and translation actions are as follows:

Original:
b2 b2 c2 b3 c3
Changed (sub):
ben 2 ben 2 c2 ben 3 c3
Changed (tr):
Ben 2 Ben 2 c2 Ben 3 c3

# ## Substitution and Encryption

You can use the translation function to shift letters to numbers or numbers to letters to achieve
a rudimentary form of encryption.

```
@AlphaNumSet = ( '111', '222', '333', '444', '555' );
#Create code for whatever reason
foreach(@AlphaNumSet){
    $_ =~ tr/[1-5]/[s-x]/;
}
```

In Listing15_04, when you print the original and the translated forms, you achieve the following
results:

Original:
111 222 333 444 555
Changed (tr):
sss ttt uuu vvv www

# ## Escape Sequences and Limiters

Regular expressions offer a number of special characters you can use to shape expressions in
interesting, effective ways. Table 15.1 provides a discussion of characters you commonly use
in regex expressions. Subsequent sections discuss these characters in detail.