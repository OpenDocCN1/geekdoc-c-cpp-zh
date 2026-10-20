
## Answers to Self-Review Exercises

31.1 a) False. Only methods declared with the @WebMethod annotation can be invoked by a web service’s clients. b) False. The proxy class is created by NetBeans when you add a web service client to the application. c) True. d) False. In the JAX-WS framework, the client must indicate whether it wants to allow the web service to maintain session information. First, you must cast the proxy object to interface type BindingProvider, then use the BindingProvider’s getRequestContext method to obtain the RequestContext object. Finally, you must use the RequestContext’s put method to set the property BindingProvider.SESSION_MAINTAIN_PROPERTY to true. e) True. f) True. g) True. h) False. A SOAP web service implicitly returns data in XML format.

31.2 a) SOAP message or SOAP envelope. b) POJO (plain old Java object) c) HTTP. d) operationName. e) serialization. f) "application/json". g) "application/xml".

## Exercises

31.3 (Phone Book Web Service) Create a RESTful web service that stores phone book entries in the database PhoneBookDB and a web client application that consumes this service. The web service should output XML. Use the steps in Section 30.2.1 to create the PhoneBook database and a data source name for accessing it. The database contains one table—PhoneBook—with three columns—LastName, FirstName and PhoneNumber. The LastName and FirstName columns store up to 30 characters. The PhoneNumber column supports phone numbers of the form (800) 555-1212 that contain 14 characters. Use the PhoneBookDB.sql script provided in the examples folder to create the PhoneBook table.

Give the client user the capability to enter a new contact (web method addEntry) and to find contacts by last name (web method getEntries). Pass only Strings as arguments to the web service. The getEntries web method should return an array of Strings that contains the matching phone book entries. Each String in the array should consist of the last name, first name and phone number for one phone book entry. These values should be separated by commas.

```
SELECT LastName, FirstName, PhoneNumber
FROM PhoneBook
WHERE (LastName = LastName)
```

The INSERT statement that inserts a new entry into the PhoneBook database should be:

```
INSERT INTO PhoneBook (LastName, FirstName, PhoneNumber)
VALUES (LastName, FirstName, PhoneNumber)
```

- 31.2 Fill in the blanks for each of the following statements:
- a) A key difference between SOAP and REST is that SOAP messages have data wrapped in a(n) ______.
- b) A web service in Java is a(n) ______—it does not need to implement any interfaces or extend any classes.
- c) Web service requests are typically transported over the Internet via the ______ protocol.
- d) To set the exposed name of a web method, use the ______ element of the @WebMethod annotation.
- e) ______ transforms an object into a format that can be sent between a web service and a client.
- f) To return data in JSON format from a method of a REST-based web service, the @Produces annotation is set to ______.
- g) To return data in XML format from a method of a REST-based web service, the @Produces annotation is set to ______.

31.4 (Phone Book Web Service Modification) Modify Exercise 31.3 so that it uses a class named PhoneBookEntry to represent a row in the database. The web service should return objects of type PhoneBookEntry in XML format for the getEntries method, and the client application should use the JAXB method unmarshal to retrieve the PhoneBookEntry objects.

31.5 (Phone-Book Web Service with JSON) Modify Exercise 31.4 so that the PhoneBookEntry class is passed to and from the web service as a JSON object. Use serialization to convert the JSON object into an object of type PhoneBookEntry.

31.6 (Blackjack Web Service Modification) Modify the Blackjack web service example in Section 31.9 to include class Card. Modify web method dealCard so that it returns an object of type Card and modify web method getHandValue so that it receives an array of Card objects from the client. Also modify the client application to keep track of what cards have been dealt by using ArrayLists of Card objects. The proxy class created by NetBeans will treat a web method’s array parameter as a List, so you can pass these ArrayLists of Card objects directly to the getHandValue method. Your Card class should include set and get methods for the face and suit of the card.

31.7 (Project: Airline Reservation Web-Service Modification) Modify the airline reservation web service in Section 31.10 so that it contains two separate methods—one that allows users to view all available seats, and another that allows users to reserve a particular seat that is currently available. Use an object of type Ticket to pass information to and from the web service. The web service must be able to handle cases in which two users view available seats, one reserves a seat and the second user tries to reserve the same seat, not knowing that it’s now taken. The names of the methods that execute should be reserve and getAllAvailableSeats.

31.8 (Project: Morse Code Web Service) In Exercise 16.22, you learned about Morse Code and wrote applications that could translate English phrases into Morse Code and vice versa. Create a SOAP-based web service that provides two methods—one that translates an English phrase into Morse Code and one that translates Morse Code into English. Next, build a Morse Code translator GUI application that invokes the web service to perform these translations.

## Making a Difference

31.9 (Project: Spam Scanner Web Service) In Exercise 16.27, you created a spam scanner application that scanned an e-mail and gave it a point rating based on the occurrence of certain words and phrases that commonly appear in spam e-mails and how many times the words and phrases occurred in the e-mail. Create a SOAP-based Spam scanner web service. Next, modify the GUI application you created in Exercise 16.27 to use the web service to scan an e-mail. Then display the point rating returned by the web service.

31.10 (Project: SMS Web Service) In Exercise 16.28, you created an SMS message-translator application. Create a SOAP-based web service with three methods:
- a) one that receives an SMS abbreviation and returns the corresponding English word or phrase,
- b) one that receives an entire SMS message and returns the corresponding English text, and
- c) one that translates English text into an SMS message.

Use the web service from a GUI application that displays the web service’s responses.

31.11 (Project: Gender-Neutrality Web Service) In Exercise 1.12, you researched eliminating sexism in all forms of communication. You then described the algorithm you’d use to read through a paragraph of text and replace gender-specific words with gender-neutral equivalents. Create a SOAP-based web service that receives a paragraph of text, then replaces gender-specific words with gender-neutral ones. Use the web service from a GUI application that displays the resulting gender-neutral text.

## Operator Precedence Chart

Operators are shown in decreasing order of precedence from top to bottom (Fig. A.1).

| Operator | Description | Associativity |
|---|---|---|
| ++ | unary postfix increment | right to left |
| -- | unary postfix decrement |  |
| ++ | unary prefix increment | right to left |
| -- | unary prefix decrement |  |
| + | unary plus |  |
| - | unary minus |  |
| ! | unary logical negation |  |
| ~ | unary bitwise complement |  |
| ( type ) | unary cast |  |
| * | multiplication | left to right |
| / | division |  |
| % | remainder |  |
| + | addition or string concatenation | left to right |
| - | subtraction |  |
| << | left shift | left to right |
| >> | signed right shift |  |
| >>> | unsigned right shift |  |
| < | less than | left to right |
| <= | less than or equal to |  |
| > | greater than |  |
| >= | greater than or equal to |  |
| instanceof | type comparison |  |
| == | is equal to | left to right |
| != | is not equal to |  |
| & | bitwise AND boolean logical AND | left to right |
| ^ | bitwise exclusive OR boolean logical exclusive OR | left to right |

Fig. A.1 | Operator precedence chart. (Part 1 of 2.)
