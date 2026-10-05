# 12.2 Templates

At whatever point you are taking information from a client, you ought to accept it. If you do not accept the client's information, it can bring about numerous issues—including conceivable security dangers.

Accepting data is not muddled. We'll go over the most widely recognized PHP functions that are utilized to disinfect information from clients. Accepting checkboxes, radio catches, and chooses Accepting information that originates from checkboxes; radio catches, and chooses is simpler than accepting free arrangement fields, for example, content boxes in light of the fact that the quality ought to be one of the predefined qualities. To guarantee this, store the majority of the alternatives in an array, and verify the client info is a piece of the array when you prepare the information. We'll take a gander at the code for checking info from a single choice (at the end of the day, and only one checkbox, radio catch, or other determination).

# Querying the Database with Form Data

Once you've approved your information, you're prepared to begin utilizing data from the structures in your database inquiries. Case 10-11 makes a function called query_db from the code in Chapter 7 for showing creators with a change to line 11 that permits coordinating the title with a LIKE inquiry condition. LIKE and NOT LIKE are for the most part utilized with strings and conceivably with special cases, for example, the underscore (_) and the percent sign (%).

+   - The underscore (_) matches a solitary character.

+   - The percent sign (%) matches zero or more characters.

In Example 10-10, the function takes a solitary parameter and hunt down the specific book title you're hoping to discover.

Sample 10.10. Consolidating structure handling and database questioning

```
1 <?php
2 function query_db($qstring) {
3 include('db_login.php');/association subtle elements
4 require_once('DB.php');/PEAR DB
```