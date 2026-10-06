```
if(\$_POST['word'])
{
  $c = mysql_connect('localhost','testapp','test123');
  mysql_select_db("testapp",$c);
  $query = "select * from wordlist where word like '%'.$_POST['word'].'%'";
  $q = mysql_query($query,\$c);
  while($row = mysql_fetch_array($q)) {
    print "{$row[0]}<BR\n";
  }
}?>
```

The search.php code begins by checking to see if the user is successfully authenticated. If the session auth flag is not set, it redirects the user back to the login page. If the user is authenticated, a form is presented to search for words. If the words field was submitted connects to the backend database server and switches to the testapp database. A query is executed to look for all words that have the submitted data as part of the word. The % symbol is a wildcard data, so it makes the query search for the data submitted anywhere in the word.

Once the query is executed, the script iterates through each returned row, and prints the output to the screen. We can see that this script also has no input sanitization, so we can take advantage of similarly to how we take advantage of the login script. Because this script is printing output to the screen, however, we have the advantage of being able to see the results of the query we are issuing to the server. We can use this script to map out the table being used to store logs, and dump the data to the screen. Let’s look at how that can be accomplished.

# Note

We have presented the code for each page we are exploiting in this chapter. When we are testing a target in a real penetration test, typically won’t have access to the script code. We included it here so that we can understand not just to break it, but also what problems lead up to the broken code.