
```php
if ($_POST['login'] && $_POST['pass'])
{
  $c = mysql_connect('localhost','testapp','test123');
  $q = mysql_query("select * from testapp.login where login = '{$_POST['login']}' and pass = '{$_POST['pass']}'");
```

```php
?>
<FORM METHOD=POST>
Login:<INPUT TYPE=TEXT NAME=login><BR>
Pass:<INPUT TYPE=PASSWORD NAME=pass><BR>
<INPUT TYPE=SUBMIT VALUE="Login!"><BR>
</FORM>
```

The PHP code from this script begins by creating a session to track information about a user in the $_SESSION array, and that information will persist across page views. If data has been submitted via the POST method, the script checks to verify that both the login and pass variables have been submitted. If not, the the script can't check whether the username and password match in the database. Next, the script connects to the MySQL database with credentials we will create in a moment. Now that the script is connected to the database, it's time to search for the input that the user submitted in the database.

The query being executed is designed to get all the records from the database where the login field in the database contains the information sent via the login field in the submission form, and the pass field matches the password field. Each piece of data is enclosed in single quote characters. This works as long as the input doesn't have a single quote in it. If it does, the single quote ending the data being searched for will be closed properly, and the rest of the submitted string will be executed as part of the query. The query returns information, the form sets an authenticated flag in the session, and sends the user to the search page. Let's finish setting up our database so that we can test this out. We are going to create a file called addsql.sql and add the following text:

```sql
create database if not exists testapp;
grant all privileges on testapp.* to testapp@localhost
identified by 'test123';
create table if not exists testapp.login (login varchar(10),
pass varchar(10));
insert into testapp.login values ('admin','admin123');
create table if not exists testapp.wordlist (word varchar(25));
insert into testapp.wordlist values ('this'), ('that'),
('now'), ('happy'), ('sad'), ('coding'), ('for'), ('pentesters'),
('ruby'), ('python');
```

To set up the database for our scripts, we need to create the database and enter sample data. The preceding SQL script creates the testapp database, and then grants privileges to that database to the testapp user with a password of test123. Next, it creates a login table with two variables, login and pass. Once the table is created, the first login is included with a login of admin and a super-secret password of admin123. Now that the authentication values are set up, we are going to want pull some data in the next example, so we will go ahead and create a table to store a list of words, and insert those words into the wordlist table.

We need to get our SQL script into the database. By saving these queries to a file, in this case addsql.sql, we can run the queries with a single command. By saving these commands to a file, we also have the added advantage of being able to build the commands with a text editor instead of using the MySQL shell, and if we need to execute these commands again we won't have to remember them. When we issue the command "mysql -u root < addsql.sql", the mysql client will take the input from the addsql.sql file we created and run it on the server. The -u option is the username we want to use. We use the less symbol to indicate that we are sending data from a file as standard input to the application. Doing the redirection makes it that we don't have to type each command individually where we might make a mistake.

Let’s take a look at our login page. After saving the page as login.php, we should be able to visit http://localhost/login.php and see the login.

The login page, we need to

The query being executed is: select * from testapp.login where login = '{$_POST['login']}' and pass = '{$_POST['pass']}'

The query being executed is designed to get all the records from the database where the login field in the database contains the information sent via the login field in the submission form, and the pass field matches the password field. Each piece of data is enclosed in single quote characters. This works as long as the input doesn't have a single quote in it. If it does, the single quote ending the data being searched for will be closed properly, and the rest of the submitted string will be executed as part of the query. The query returns information, the form sets an authenticated flag in the session, and sends the user to the search page.

Let's finish setting up our database so that we can test this out. We are going to create a file called addsql.sql and add the following text:

The login page, we need to

The query being executed is: select * from testapp.login where login = '{$_POST['login']}' and pass = '{$_POST['pass']}'

The query being executed is designed to get all the records from the database where the login field in the database contains the information sent via the login field in the submission form, and the pass field matches the password field. Each piece of data is enclosed in single quote characters. This works as long as the input doesn't have a single quote in it. If it does, the single quote ending the data being searched for will be closed properly, and the rest of the submitted string will be executed as part of the query. The query returns information, the form sets an authenticated flag in the session, and sends the user to the search page.

The login page, we need to

The login page, we need to

The login page, we need to

### search.php: Returning extra records

```php
<?php
session_start();
if($_SESSION['authed'] != 1)
{
  header('Location: login.php');
  exit();
}
?>
<FORM METHOD=POST>
Search for:
Search Results:<BR>
<?php
```php
if($_POST['word'])
{
  $c = mysql_connect('localhost','testapp','test123');
  mysql_select_db("testapp",$c);
  $query = "select * from wordlist where word like '%'.$_POST['word'].%'";
  $q = mysql_query($query,$c);
  while($row = mysql_fetch_array($q)) {
    print "{$row[0]}<BR>\n";
  }
}?>
```

The search.php code begins by checking to see if the user is successfully authenticated. If the session auth flag is not set, it redirects the user back to the login page. If the user is authenticated, a form is presented to search for words. If the words field was submitted connects to the backend database server and switches to the testapp database. A query is executed to look for all words that have the submitted data as part of the word. The % symbol is a wildcard data, so it makes the query search for the data submitted anywhere in the word.

Once the query is executed, the script iterates through each returned row, and prints the output to the screen. We can see that this script also has no input sanitization, so we can take advantage of similarly to how we take advantage of the login script. Because this script is printing output to the screen, however, we have the advantage of being able to see the results of the query we are issuing to the server. We can use this script to map out the table being used to store logs, and dump the data to the screen. Let’s look at how that can be accomplished.

# Note

We have presented the code for each page we are exploiting in this chapter. When we are testing a target in a real penetration test, typically won’t have access to the script code. We included it here so that we can understand not just to break it, but also what problems lead up to the broken code.
