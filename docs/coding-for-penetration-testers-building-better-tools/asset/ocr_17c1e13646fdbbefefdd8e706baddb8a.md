```
if ($_POST['login'] && $_POST['pass'])
{
  $c = mysql_connect('localhost','testapp','test123');
  $q = mysql_query("select * from testapp.login where login = '\${\_POST['login']}\' and pass = '\${\_POST['pass']}\'\
```

```
?>
<FORM METHOD=POST>
Login:<INPUT TYPE=TEXT NAME=login><BR>
Pass:<INPUT TYPE=PASSWORD NAME=pass><BR>
<INPUT TYPE=SUBMIT VALUE="Login!"><BR>
</FORM>
```

The PHP code from this script begins by creating a session to track information about a user in the $_SESSION array, and that information will persist across page views. If data has been submitted via the POST method, the script checks to verify that both the login and pass variables have been submitted. If not, the script can't check whether the username and password match in the database. Next, the script connects to the MySQL database with credentials we will create in a moment. Now that the script is connected to the database, it's time to search for the input that the user submitted in the database.

The query being executed is designed to get all the records from the database where the login field in the database contains the information sent via the login field in the submission form, and the pass field matches the password field. Each piece of data is enclosed in single quote characters. This works as long as the input doesn't have a single quote in it. If it does, the single quote ending the data being searched for will be closed properly, and the rest of the submitted string will be executed as part of the query. The query returns information, the form sets an authenticated flag in the session, and sends the user to the search page. Let's finish setting up our database so that we can test this out. We are going to create a file called addsql.sql and add the following text: