an array of output lines. Because wmic starts with headers, we'll go from the third line until end and split our CSV values. We'll assign those to an array called userinfo.

We also want to know if a user is online. To do this, we can query the HKEY_USER registry keys. The HKEY_USER hive will have the user's who are currently online mapped to their ntuser.dat hive. When we pull the list of SIDs there, we can see if the SID for the current user are active. We use the registry_exits function to be looking at HKEY_USER and if it does, we know they are online and so will set that value in our userinfo array. We append that userinfo array to the end of the users array.

Next we create a table and specify the Header, our indentation, and list the columns we will be printing. This sets the table up so that from this point on, all we have to add rows, and Metasplit handle formatting the table for us. When we add the rows we use the map function to go through each of the users and we build the fully qualified username and append a row to the end of the table that has the username, whether or not the user is active, and the sid.

With our table built, the print_line function will turn the table into a string and print it out the screen for us. We also want to save this output for use later. With Metasploit, we have the ability to use the store_loot functions to handle this for us. The store_loot function takes a number of options: the type of data being saved, what the mime-type of data is, the host that it came from, the data itself, and a short description of what that data is. This will add a file to the filesystem with our output in it as well as updating the Metasploit database if the database is connected. Finally we end our function, having executed all queries and save the data.

Next we need to create our code to list group information. We are going to call this function get_group and we are going to go through a similar pattern, only we need to combine the output from two different commands to get the data we need.

```
def get_group
groups = []
    data = wmic_query('group') list brief
```