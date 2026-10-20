```
75 // private class that contains the message we are receiving
76 class TextMessage
77 {
78     private String message; // message we're receiving
79
80     // returns the message
81     public String getMessage()
82     {
83         return message;
84     } // end method getMessage
85
86     // sets the message
87     public void setMessage( String value )
88     {
89         message = value;
90     } // end method setMessage
91 } // end class TextMessage
```

Fig. 31.16 | Client that consumes the WelcomeRESTJSON service. (Part 3 of 3.)

Lines 83–84 create the URL String that is used to invoke the web service. Lines 87–88 create a URL object using this String, then call the URL’s openStream method to invoke the web service and obtain an InputStream from which the client can read the response. The InputStream is wrapped in an InputStreamReader so it can be passed as the first argument to the Gson class’s fromJson method. This method is overloaded. The version we use takes as arguments a Reader from which to read a JSON String and a Class<T> object indicating the Java class to which the JSON String will be converted (line 92). In this example, the JSON String contains a TextMessage object, so we use the Java compiler shortcut TextMessage.class to create the Class<TextMessage> object we need as the second argument. Lines 95–96 display the message in the TextMessage object.

The TextMessage classes in the web service and client are unrelated. Technically, the client can be written in any programming language, so the manner in which a response is processed can vary greatly. Since our client is written in Java, we duplicated the TextMessage class in the client so we could easily convert the JSON object back to Java.

# 31.9 Session Tracking in a SOAP Web Service

Section 29.8 described the advantages of using session tracking to maintain client-state information so you can personalize the users’ browsing experiences. Now we’ll incorporate session tracking into a web service. Suppose a client application needs to call several methods from the same web service, possibly several times each. In such a case, it can be beneficial for the web service to maintain state information for the client, thus eliminating the need for client information to be passed between the client and the web service multiple times. For example, a web service that provides local restaurant reviews could store the client user’s street address during the initial request, then use it to return personalized, localized results in subsequent requests. Storing session information also enables a web service to distinguish between clients.