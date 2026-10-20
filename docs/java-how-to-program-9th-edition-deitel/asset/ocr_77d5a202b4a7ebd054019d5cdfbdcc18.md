31.4 (Phone Book Web Service Modification) Modify Exercise 31.3 so that it uses a class named PhoneBookEntry to represent a row in the database. The web service should return objects of type PhoneBookEntry in XML format for the getEntries method, and the client application should use the JAXB method unmarshal to retrieve the PhoneBookEntry objects.

31.5 (Phone-Book Web Service with JSON) Modify Exercise 31.4 so that the PhoneBookEntry class is passed to and from the web service as a JSON object. Use serialization to convert the JSON object into an object of type PhoneBookEntry.

31.6 (Blackjack Web Service Modification) Modify the Blackjack web service example in Section 31.9 to include class Card. Modify web method dealCard so that it returns an object of type Card and modify web method getHandValue so that it receives an array of Card objects from the client. Also modify the client application to keep track of what cards have been dealt by using ArrayLists of Card objects. The proxy class created by NetBeans will treat a web method’s array parameter as a List, so you can pass these ArrayLists of Card objects directly to the getHandValue method. Your Card class should include set and get methods for the face and suit of the card.

31.7 (Project: Airline Reservation Web-Service Modification) Modify the airline reservation web service in Section 31.10 so that it contains two separate methods—one that allows users to view all available seats, and another that allows users to reserve a particular seat that is currently available. Use an object of type Ticket to pass information to and from the web service. The web service must be able to handle cases in which two users view available seats, one reserves a seat and the second user tries to reserve the same seat, not knowing that it’s now taken. The names of the methods that execute should be reserve and getAllAvailableSeats.

31.8 (Project: Morse Code Web Service) In Exercise 16.22, you learned about Morse Code and wrote applications that could translate English phrases into Morse Code and vice versa. Create a SOAP-based web service that provides two methods—one that translates an English phrase into Morse Code and one that translates Morse Code into English. Next, build a Morse Code translator GUI application that invokes the web service to perform these translations.

# Making a Difference

31.9 (Project: Spam Scanner Web Service) In Exercise 16.27, you created a spam scanner application that scanned an e-mail and gave it a point rating based on the occurrence of certain words and phrases that commonly appear in spam e-mails and how many times the words and phrases occurred in the e-mail. Create a SOAP-based Spam scanner web service. Next, modify the GUI application you created in Exercise 16.27 to use the web service to scan an e-mail. Then display the point rating returned by the web service.

31.10 (Project: SMS Web Service) In Exercise 16.28, you created an SMS message-translator application. Create a SOAP-based web service with three methods:

+   a) one that receives an SMS abbreviation and returns the corresponding English word or phrase,
+   b) one that receives an entire SMS message and returns the corresponding English text, and
+   c) one that translates English text into an SMS message.

Use the web service from a GUI application that displays the web service’s responses.

31.11 (Project: Gender-Neutrality Web Service) In Exercise 1.12, you researched eliminating sexism in all forms of communication. You then described the algorithm you’d use to read through a paragraph of text and replace gender-specific words with gender-neutral equivalents. Create a SOAP-based web service that receives a paragraph of text, then replaces gender-specific words with gender-neutral ones. Use the web service from a GUI application that displays the resulting gender-neutral text.