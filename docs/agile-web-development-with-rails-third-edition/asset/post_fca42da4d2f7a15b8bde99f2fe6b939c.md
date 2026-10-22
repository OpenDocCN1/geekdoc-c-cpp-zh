
In this chapter, we’ll see

- adding virtual attributes to models,
- using more validations,
- coding forms without underlying models,
- implementing one-action form handling,
- adding authentication to a session,
- using script/console,
- using database transactions, and
- writing an Active Record hook.

## Chapter 11

### Task F: Administration

We have a happy customer—in a very short time we’ve jointly put together a basic shopping cart that she can start showing to her users. There’s just one more change that she’d like to see. Right now, anyone can access the administrative functions. She’d like us to add a basic user administration system that would force you to log in to get into the administration parts of the site.

We’re happy to do that, because it gives us a chance to look at virtual attributes and filters, and it lets us tidy up the application somewhat.

Chatting with our customer, it seems as if we don’t need a particularly sophisticated security system for our application. We just need to recognize a number of people based on usernames and passwords. Once recognized, these folks can use all of the administration functions.

### 11.1 Iteration F1: Adding Users

Let’s start by creating a model and database table to hold our administrators’ usernames and passwords. Rather than store passwords in plain text, we’ll feed them through an SHA1 digest, resulting in a 160-bit hash. We check a user’s password by digesting the value they give us and comparing that hashed value with the one in the database. This system is made even more secure by salting the password, which varies the seed used when creating the hash by combining the password with a pseudorandom string.¹

```
depot> ruby script/generate scaffold \
  user name:string hashed_password:string salt:string
```

Since this modified config/routes.rb, which is cached for performance reasons, you will need to restart your server.

> 1. For other recipes on how to do this, see the Authentication and Role-Based Authentication sections in Chad Fowler’s Rails Recipes [Fow06].

Once that's done, let's look at the migration that's generated:

```
Download depot_p/db/migrate/20080601000007_create_users.rb
class CreateUsers < ActiveRecord::Migration
  def self.up
    create_table :users do |t|
      t.string :name
      t.string :hashed_password
      t.string :salt

      t.timestamps
    end
  end

  def self.down
    drop_table :users
  end
end
```

Now run the migration as usual:

```
depot> rake db:migrate
```

Now we have to flesh out the user model. This turns out to be fairly complex because it has to work with the plain-text version of the password from the application's perspective but maintain a salt value and a hashed password in the database. Let's look at the model in sections. First, here's the validation:

```
Download depot_p/app/models/user.rb
class User < ActiveRecord::Base

  validates_presence_of  :name
  validates_uniqueness_of :name

  attr_accessor :password_confirmation
  validates_confirmation_of :password

  validate :password_non_blank

private

  def password_non_blank
    errors.add(:password, "Missing password") if hashed_password.blank?
  end
end
```

That's a fair amount of validation for such a simple model. We check that the name is present and unique (that is, no two users can have the same name in the database). Then there's the mysterious validates_confirmation_of declaration.

You know those forms that prompt you to enter a password and then make you reenter it in a separate field so they can validate that you typed what you thought you typed? Well, Rails can automatically validate that the two

passwords match. We'll see how that works in a minute. For now, we just have to know that we need two password fields, one for the actual password and the other for its confirmation.

Finally, we check that the password has been set. But we don't check the password attribute itself. Why? Because it doesn't really exist—at least not in the database. Instead, we check for the presence of its proxy, the hashed password. But to understand that, we have to look at how we handle password storage.

First let's see how to create a hashed password. The trick is to create a unique salt value, combine it with the plain-text password into a single string, and then run an SHA1 digest on the result, returning a 40-character string of hex digits. We'll write this as a private class method. (We'll also need to remember to require the digest/sha1 library in our file. See the listing starting on page 163 to see where it goes.)

```
Download depot_p/app/models/user.rb
def self.encrypted_password(password, salt)
  string_to_hash = password + "wibble" + salt
  Digest::SHA1.hexdigest(string_to_hash)
end
```

We'll create a salt string by concatenating a random number and the object id of the user object. It doesn't much matter what the salt is as long as it's unpredictable (using the time as a salt, for example, has lower entropy than a random string). We store this new salt into the model object's salt attribute. Again, this is a private method, so place it after the private keyword in the source:

```
Download depot_p/app/models/user.rb
def create_new_salt
  self.salt = self.object_id.to_s + rand.to_s
end
```

There's a subtlety in this code we haven't seen before. Note that we wrote self.salt =.... This forces the assignment to use the salt= accessor method—we're saying "call the method salt in the current object." Without the self., Ruby would have thought we were assigning to a local variable, and our code would have no effect.²

2. Although using the instance variable directly would achieve the correct results, it would also tie you to a representation that may not always be the same. The attribute salt/salt= is the "official" interface to the underlying model attributes, so it is better to use them rather than instance variables. Another way of looking at it is that because the attributes form part of the public interface of the class, then the class should eat its own dog food and use that interface too. If you use @xx internally and .xx externally, the door is wide open for some kind of mismatch down the road.

Now we need to write some code so that whenever a new plain-text password is stored into a user object we automatically create a hashed version (which will get stored in the database). We'll do that by making the plain-text password a *virtual attribute* of the model—it looks like an attribute to our application, but it isn't persisted into the database.

If it weren't for the need to create the hashed version, we could do this simply using Ruby's attr_accessor declaration:

```
attr_accessor :password
```

Behind the scenes, attr_accessor generates two accessor methods: a reader called password and a writer called password=. The fact that the writer method name ends in an equals sign means that it can be assigned to. So, rather than using standard accessors, we'll simply implement our own public methods and have the writer also create a new salt and set the hashed password:

```
def password
  @password
end

def password=(pwd)
  @password = pwd
  return if pwd.blank?
  create_new_salt
  self.hashed_password = User.encrypted_password(self.password, self.salt)
end
```

There's one last change. Let's write a public class method that returns a user object if the caller supplies the correct name and password. Because the incoming password is in plain text, we have to read the user record using the name as a key and then use the salt value in that record to construct the hashed password again. We then return the user object if the hashed password matches. We can use this method to authenticate a user.

```
def self.authenticate(name, password)
  user = self.find_by_name(name)
  if user
    expected_password = encrypted_password(password, user.salt)
    if user.hashed_password != expected_password
      user = nil
    end
  end
  user
end
```

This code uses a clever little Active Record trick. You see that the first line of the method calls find_by_name. But we don't define a method with that name.
