```
26
27     // return the email String
28     public String getEmail()
29     {
30         return email;
31     } // end method getEmail
32
33     // set the email String
34     public void setEmail( String email )
35     {
36         this.email = email;
37     } // end method setEmail
38
39     // return the phone String
40     public String getPhone()
41     {
42         return phone;
43     } // end method getPhone
44
45     // set the phone String
46     public void setPhone( String phone )
47     {
48         this.phone = phone;
49     } // end method setPhone
50
51     // returns result for rendering on the client
52     public String getResult()
53     {
54         if ( name != null && email != null && phone != null )
55             return "<p style=\"background-color:yellow;width:200px;\" + 
56                 "padding:5px\"><Name: " + getName() + "<br/>E-Mail: " + 
57                 getEmail() + "<br/>Phone: " + getPhone() + "</p>";
58         else
59             return ""; // request has not yet been made
60     } // end method getResult
61 } // end class ValidationBean
```

Fig. 29.15 | ValidationBean stores the validated data, which is then used as part of the response to the client. (Part 2 of 2.)

# index.xhtml

Figure 29.16 shows this app’s index.xhtml file. The initial request to this web app displays the page shown in Fig. 29.16(a). When this app is initially requested, the beginning of the JSF application lifecycle uses this index.xhtml document to build the app’s facelets view and sends it as the response to the client browser, which displays the form for user input. During this initial request, the EL expressions (lines 22, 30, 39 and 49) are evaluated to obtain the values that should be displayed in various parts of the page. Nothing is displayed initially as a result of these four EL expressions being evaluated, because no default values are specified for the bean’s properties. The page’s h:form element contains an h:panelGrid (lines 18–45) with three columns and an h:commandButton (line 46), which by default submits the contents of the form’s fields to the server.