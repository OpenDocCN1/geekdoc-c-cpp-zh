This is dangerous. Imagine a malicious user manually sending the string "' OR 1 --" as the subject parameter. After Rails substituted this into the SQL it generates for the find method, the resulting statement will look like this:¹

```
select * from emails where owner_id = 123 AND subject = '' OR 1 --'
```

The OR 1 condition is always true. The two minus signs start a SQL comment; everything after them will be ignored. Our malicious user will get a list of all the e-mails in the database.²

# Protecting Against SQL Injection

If you use only the predefined Active Record functions (such as attributes, save, and find) and if you don't add your own conditions, limits, and SQL when invoking these methods, then Active Record takes care of quoting any dangerous characters in the data for you. For example, the following call is safe from SQL injection attacks:

```
order = Order.find(params[:id])
```

Even though the id value comes from the incoming request, the find method takes care of quoting metacharacters. The worst a malicious user could do is to raise a Not Found exception.

But if your calls do include conditions, limits, or SQL and if any of the data in these comes from an external source (even indirectly), you have to make sure that this external data does not contain any SQL metacharacters. Some potentially insecure queries include the following:

```
Email.find(:all,
  :conditions => "owner_id = 123 AND subject = '#{params[:subject]}'")
```

```
Users.find(:all,
  :conditions => "name like '%#{session[:user].name}%'")
```

```
Orders.find(:all,
  :conditions => "qty > 5",
  :limit      => #{params[:page_size]})
```

The correct way to defend against these SQL injection attacks is never to substitute anything into a SQL statement using the conventional Ruby #{...} mechanism. Instead, use the Rails bind variable facility. For example, you'd want to rewrite the web mail search query as follows:

```
subject = params[:subject]
Email.find(:all,
  :conditions => ["owner_id = 123 AND subject = ?", subject ])
```

1. The actual attacks used depend on the database. These examples are based on MySQL.
2. Of course, the owner id would have been inserted dynamically in a real application; this was omitted to keep the example simple.