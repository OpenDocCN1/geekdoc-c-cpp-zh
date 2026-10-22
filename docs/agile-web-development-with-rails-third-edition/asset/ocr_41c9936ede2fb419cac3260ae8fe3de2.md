This chapter is an adaptation and extension of Andreas Schwarz’s online manual on Rails security. This was available at http://manuals.rubyonrails.com/read/book/8 (but the site appears to be down at time of printing).

# Chapter 27

# Securing Your Rails Application

Applications on the Web are under constant attack. Rails applications are not exempt from this onslaught.

Security is a big topic—the subject of whole books. We can’t do it justice in just one chapter. You’ll probably want to do some research before you put your applications on the scary, mean ‘net. A good place to start reading about security on the Web is the Open Web Application Security Project (OWASP) at http://www.owasp.org/. It’s a group of volunteers who put together “free, professional-quality, open-source documentation, tools, and standards” related to security. Be sure to check out their top ten list of security issues in web applications. If you follow a few basic guidelines, you can make your Rails application a lot more secure.

# 27.1 SQL Injection

SQL injection is the number-one security problem in many web applications. So, what is SQL injection, and how does it work?

Let’s say a web application takes strings from unreliable sources (such as the data from web form fields) and uses these strings directly in SQL statements. If the application doesn’t correctly quote any SQL metacharacters (such as backslashes or single quotes), an attacker can take control of the SQL executed on your server, making it return sensitive data, create records with invalid data, or even execute arbitrary SQL statements.

Imagine a web mail system with a search capability. The user could enter a string on a form, and the application would list all the e-mails with that string as a subject. Inside our application’s model there might be a query that looks like the following:

```
Email.find(:all,
    :conditions => "owner_id = 123 AND subject = '#{params[:subject]}'")
```