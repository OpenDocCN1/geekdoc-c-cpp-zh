To be able to implement the security policy, we need to be able to have a mechanism for recognizing which users have roles other than the default logged-in user role. To do that, we add a new type to the datastore: a UserRole type. The role type is just a username (the name of the logged-in user as returned by the login service), and a string containing the user's role. A basic implementation of the type and a function to retrieve a user's role is shown below:

Download secure-chat/chat.py

```
~~~python
class UserRole(db.Model):
    name = db.StringProperty(required=True)
    role = db.StringProperty(choices=["User", "admin", "privileged"],
                             default="User")

    @staticmethod
    def GetUserRole(name):
        user_record = db.GqlQuery("SELECT * from UserRole WHERE " +
                                  "name = :1",
                                  name).get()

        if user_record != None:
            return user_record.role
        else:
            return "User"
~~~
```

This is very straightforward code: the class is a standard datastore type with two string fields. By annotating the role field with a specific list of possible values, only those roles will be permitted. It will be impossible for anyone, either through a mistake or through a deliberate attack to create a user with an invalid role. And any user who isn't in the datastore with a UserRole record will fall through the check and will therefore end up with the default role User.

That defaulting rule is enforced by GetUserRole, which returns the role for a specific user. If a user wasn't granted a specific role, then they won't have an entry in the UserRole table, and so the GQL query will end up raising an IndexError. When that happens, GetUserRole will end up running the exception-handling code, which returns the default role, User.

The one interesting thing about this code is the use of limited values for the role property. Instead of making role be a plain unrestricted string property, we specifically limited it to make sure that the user has a valid role; there is no possible way that GetUserRole will return anything other than the three valid roles recognized by the application. It might not seem important: but when you're doing security, it is absolutely