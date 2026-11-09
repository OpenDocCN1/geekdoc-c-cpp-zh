of a request to contain HTML markup, and then, using that markup, to provide JavaScript code.

For example, what would happen if a user were to send a chat message containing the following?

Hi there `<script language="javascript"> print("JavaScript!");</script>`

A user's display would show the chat message "Hi there, JavaScript!"—but the JavaScript code that prints the word "JavaScript" would execute on the user's computer.

There's also a closely related kind of cross-site scripting attack that tries to run code on a server. The most common form of this is called SQL injection. SQL injection, specifically, isn't a problem for App Engine (since you don't use SQL), but it's a good example of a general type of attack.

In a SQL injection attack, an attacker sends a string to a form that will be used as a field in a query. For example, in many systems, when users log in, they'll be asked for their usernames and passwords in a form, and then the system will perform a SQL query to retrieve the correct password. It'll do a query like: `SELECT password FROM Users WHERE name=$1`. Then a user can provide a username like `me;DROP TABLE *`. If the user's username field value is used directly in the query, that will execute: `SELECT password FROM User WHERE name = me; DROP TABLE *`. By knowing that the string was going to be passed directly into a SQL query, an attacker can create a string that will execute other, damaging SQL commands.

The way to protect against both of these attacks is clear: always clean your inputs. That is, when you get an input from a user, always take it, and put it through a cleaning process that eliminates any metacharacters. To prevent someone from injecting JavaScript into your HTML, you need to make sure that any < characters are replaced with XML literal characters like `&lt;`. To prevent someone from injecting SQL, you need to make sure that your input doesn't contain things like quotes, query-metacharacters, or statement terminators; if it does, they need to be escaped.

App Engine provides tools that you can use to protect against this kind of XSS attack. If you're using Python, there's a function in the cgi module of the webapp framework. Just invoke `cgi.escape(input_string)`, and you don't need to worry about this kind of XSS. In your templates, you can also do escaping on the output side by attaching a filter; if you