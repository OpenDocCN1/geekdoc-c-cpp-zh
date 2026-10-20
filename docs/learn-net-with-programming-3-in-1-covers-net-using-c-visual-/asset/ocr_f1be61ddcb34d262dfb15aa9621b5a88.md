```
[webservicebinding(conformsto=
wsiprofiles.basicprofile1_1)]  to  [webservicebinding
(conformsto = wsiprofiles.None)].

1.  [webmethod]
2.  Public int sumofnums(int firstnumber, int secondnumber)
3.  {
4.  Return firstnumber + secondnumber;
5.  }
6.
7.  //here we will use messagename property to do the differentiation between both of the methods.
8.  [webmethod(messagename = "sumoffloats")]
9.  9.
10. Public float sumofnums(float firstnumber, float secondnumber)
11. {
12. Return firstnumber + secondnumber;
13. }
```

If we want to call the Web service from the Script, we will use ASP.NET, AJAX and uncomment the below line.

```
[System.Web.Script.Services.scriptservice]

[webmethod]
```

This attribute is always used at the top of the method. We write this attribute in the Web Service. [webmethod] attribute is used to define that the method used this attribute is exposed to the user/client access.