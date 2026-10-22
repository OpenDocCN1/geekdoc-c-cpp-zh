When you refresh your browser, the template will generate the following HTML:

```
<ul>
<li>Addition: 3 </li>
<li>Concatenation: cowboy </li>
<li>Time in one hour: Fri May 23 14:30:32 -0400 2008 </li>
</ul>
```

In the browser window, you'll see something like the following:

+   - Addition: 3
+   - Concatenation: cowboy
+   - Time in one hour: Fri May 23 14:30:32 -0400 2008

In addition, stuff in .html.erb files between <% and %> (without an equals sign) is interpreted as Ruby code that is executed with no substitution back into the output. Interestingly, this kind of processing can be intermixed with non-Ruby code. For example, we could make a festive version of hello.html.erb:

```
<% 3.times do %>
Ho!<br />
<% end %>
Merry Christmas!
```

This will generate the following HTML:

Download erb/ex2.op

```
Ho!<br />

Ho!<br />

Ho!<br />

Merry Christmas!
```

Note how the text in the file within the Ruby loop is sent to the output stream once for each iteration of the loop.

But something strange is going on here, too. Where did all the blank lines come from? They came from the input file. If you think about it, the original file contains an end-of-line character (or characters) immediately after the %> of both the first line and the third line of the file. So, the <% 3.times do %> is stripped out of the file, but the newline remains. Each time around the loop, this newline is added to the output file, along with the full text of the Ho! line. This accounts for the blank line before each Ho! line in the output. Similarly, the newline after <% end %> accounts for the blank line between the last Ho! line and the Merry Christmas! line.

Normally, this doesn't matter, because HTML doesn't much care about whitespace. However, if you're using this templating mechanism to create e-mails or HTML within <pre> blocks, you'll want to remove these blank lines. Do this