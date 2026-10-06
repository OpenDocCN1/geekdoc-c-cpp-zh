
```
}
>
```

Our form is going to have two different pieces of data to submit. One is going to be the command we want to execute, and the other is going to be the output we already have and want to keep track of. We begin our script by looking for the command key being set in our POST data. If it is set, we have work to do and if it isn't, life is easy since we just have to print out a form. Once we have a command to execute, we look at the out key of the POST data to determine if there is previous output. If there is, we set our $out variable to the previous data and append a new line so that we know the difference between the commands.

If we keep the output forever, as we went along our script execution would start to take longer and longer to submit, and may look strange in server logs, so we want to truncate our string to 2000 characters. That will give us enough data to have scroll-back buffer to see what we did last, but not so much as to see what we 3 hours ago. We check the string length, and if it is greater than 2000 characters, we will take the last 2000 characters of our output and set our $out variable to that. We do this by using the substr function which takes a substring of the string, specified as the first variable, and then takes the data starting from the position indicated in the second variable passed to substr. The third variable is how many characters we want to be included in our substring. We specify out our string, the string length minus 2000 as our starting point, and 2000 characters as our length to ensure that we take the last 2000 characters.

Now that we have our previous output handled, we add the command that was submitted to the output so that we will be able to see what command executed to generate our output. We preface it with a > symbol to know that it was the command and not part of the output, and follow it with the command submitted by the form. Next, we use the exec function to execute the submitted command, and store the output in the $out variable. Because we just want to take the array and merge all the lines into a string, we can use the implode function and join all our array lines with newline characters to create a single string containing the output of our command. We append that onto the output variable $out. We now have our command executed, and the output is stored in a variable, so now that we've done the hard part, let's build a form.

```
<FORM METHOD=POST>
<TEXTAREA name=out id=out style="width: 100%; height:90%">
<?php echo $out?>
</TEXTAREA><BR>
Input Command: <INPUT NAME=command id=command TYPE=TEXT LENGTH=255>
<INPUT TYPE=SUBMIT>
</FORM>
```

We begin by creating our form. We specify that our submit method is going to be POST, and by not specifying an action, we indicate that we will send the form to itself. This will allow us to embed this code in other applications. Next, we create textarea where we will store the output. We specify a name of out, the variable we referenced earlier in our form handling code. We specify that the element ID is out as, and then we set up some basic style elements for our textarea. We want the textarea to take up most of the screen, so we specify the width as 100% of the width of the browser and the height as 90% of the browser. This will allow us to resize the browser and the form will still look right. For the data that will be included in our textarea, we open a PHP block and echo out $out variable that we built earlier. This will place our output in the textarea so that we can see it after each submission. Once we close our textarea, we need a way to submit it input that we will call command and give it a length of 255 characters. The only we're missing is a submit button, so we add one of those and our form is done.

We now have a fully functional PHP shell. However, Web pages that force us to scroll down to a certain point on the page and click a field are a pain. Let's fix that so we don't have to hate ourselves. With some basic JavaScript, we can make our form much easier to use. Let's add some finishing touches to our script.

```
<script>
var ta = document.getElementById('out');
ta.scrollTop = ta.scrollHeight;
var cmd = document.getElementById('command');
cmd.focus();
</script>
```

We use a script tag to indicate to the browser that we will be including a JavaScript code. When we gave our elements IDs earlier, it was so that we could easily reference them in our JavaScript. We create a new JavaScript variable using the var keyword and name it ta. We want ta to be the HTML element of our textarea, and the easiest way to reference it is by telling the Document Object Model of the DOM to find our element for us. It is an application interface for an HTML document that will allow us to query document properties and manipulate values. By assigning ta to our textarea box, we will have the ability to modify properties. The first thing we want to do is to set the textarea to be at the bottom of the screen. To do this, we set the ScrollTop property of ta to be equal to the scrollTop which scrolls our textarea to the bottom of the textarea. This will ensure that as we submit new commands, they are always visible.

The second thing we want to do is to put our cursor into the command text box each time the page loads. To do this, we create a cmd variable and set it equal to our command input box. Our input box has a method associated with it, called focus, which causes the cursor to be placed in the input box. We execute this method so that each time the page loads we can start typing and be in the right place on the form. This out with and without the script included to see the difference. Your output should look like Fig. 5.11.

```
$ head /etc/passwd
root:x:0:0:root:/root:/usr/sbin/nologin
deemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin/sync
games:x:5:60:games:/usr/games
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
```

FIGURE 5.11 The output of our shell.php script when using the command “head /etc/passwd.”

# Summary

We have progressed from building some simple PHP all the way to having a working shell. Through exploring form handling, conditionals, command execution, and loops, we have built file downloaders and scripts to help enumerate through server information. You should now have the PHP background to be able to take these tasks and apply them in Chapter 9, Exploitation scripting, as well as apply these techniques to real-world penetration testing scenarios. While we have just scratched the surface on all the functionality of PHP, you now know enough of the basics to work through the rest on your own time. To study more of the functionality of PHP, go to the PHP website at www.php.net. From there, you can investigate the PHP functions we already looked at and find the online documentation of the PHP language.

# CHAPTER 6

# Manipulating Windows with PowerShell

### Abstract
This chapter delves deeper into the capabilities of PowerShell, which can be very handy in certain penetration testing situations. PowerShell has access to all the functionalities of .NET and can give us capabilities that we might not otherwise have in such an environment without needing to upload tools to the system. We go over execution policies, taking control of the processes on the system, interfacing with the event logs, tweaking the Registry, and more, all through the tools tools provided by the operating system.

### Keywords
PowerShell; penetration testing; .NET; execution policies; processes; registry

# INFORMATION IN THIS CHAPTER

- Dealing With Execution Policies in PowerShell
- Penetration Testing Uses for PowerShell
- PowerShell and Metasploit

Up until a few years ago, PowerShell was just a systems administration utility. When the Pen Tester community learned more about the tool, it has become one of the most powerful tools for both pen testers and malicious attackers. PowerShell is an incredibly flexible tool that has built-in functions that support systems administration, interaction with remote systems, and can even access
