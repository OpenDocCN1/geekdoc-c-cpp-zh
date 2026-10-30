This is more than an example of a class that has too many responsibilities; it is also an example of a single method that has too many responsibilities. By reading the code carefully, you can discern what this class is trying to achieve:

+   1. It reads every line from a Stream parameter, storing each line in a list of strings.
+   2. It parses out individual fields from each line and stores them in a more structured list of Trade-Record instances.
+   3. The parsing includes some validation and some logging to the console.
+   4. Each TradeRecord is enumerated, and a stored procedure is called to insert the trades into a database.

The responsibilities of the TradeProcessor are reading streams, parsing strings, validating fields, logging, and database insertion. The single responsibility principle states that this class, like all others, should have only a single reason to change. However, the reality of the TradeProcessor is that it will change under the following circumstances:

+   - When you decide not to use a Stream for input but instead read the trades from a remote call to a web service.
+   - When the format of the input data changes, perhaps with the addition of an extra field indicating the broker for the transaction.
+   - When the validation rules of the input data change.
+   - When the way in which you log warnings, errors, and information changes. If you are using a hosted web service, writing to the console would not be a viable option.
+   - When the database changes in some way—perhaps the insert_trade stored procedure requires a new parameter for the broker, too, or you decide not to store the data in a relational database and opt for document storage, or the database is moved behind a web service that you must call.

For each of these changes, this class would have to be modified. Furthermore, unless you maintain a variety of versions, there is no possibility of adapting the TradeProcessor so that it is able to read from a different input source, for example. Imagine the maintenance headache when you are asked to add the ability to store the trades in a web service, but only if a certain command-line argument was supplied.