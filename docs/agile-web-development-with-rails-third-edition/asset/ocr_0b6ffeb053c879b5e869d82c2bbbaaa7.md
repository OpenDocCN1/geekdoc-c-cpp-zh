# 27.2 Creating Records Directly from Form Parameters

Let's say you want to implement a user registration system. Your users table looks like this:

```
create_table :users do |t|
  t.string :name
  t.string :password
  t.string :role,      :default => "user"
  t.integer :approved, :default => 0
end
```

The role column contains one of admin, moderator, or user, and it defines this user's privileges. The approved column is set to 1 once an administrator has approved this user's access to the system.

The corresponding registration form's HTML looks like this:

```
<form method="post" action="http://website.domain/user/register">
  <input type="text" name="user[name]" />
  <input type="text" name="user[password]" />
</form>
```

Within our application's controller, the easiest way to create a user object from the form data is to pass the form parameters directly to the create method of the User model:

```
def register
  User.create(params[:user])
end
```

But what happens if someone decides to save the registration form to disk and play around by adding a few fields? Perhaps they manually submit a web page that looks like this:

```
<form method="post" action="http://website.domain/user/register">
  <input type="text" name="user[name]" />
  <input type="text" name="user[password]" />
  <input type="text" name="user[role]"      value="admin" />
  <input type="text" name="user[approved]" value="1" />
</form>
```

Although the code in our controller intended only to initialize the name and password fields for the new user, this attacker has also given himself administrator status and approved his own account.

Active Record provides two ways of securing sensitive attributes from being overwritten by malicious users who change the form. The first is to list the attributes to be protected as parameters to the attr_protected method. Any attribute flagged as protected will not be assigned using the bulk assignment of attributes by the create and new methods of the model.