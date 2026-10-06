we use the establish_connection method of the ActiveRecord Base class. We pass in three named options: the adapter we will use, the username, and the database we connect to. In this case, we will continue to use our PostgreSQL connection and use "test" as the username, the password, and the database name. We now have set up our connection to the database. Further actions with ActiveRecord won't have to specify any of this information; it will be implied.

Let's set a wrapper around the people table. We did something subtle to prepare for this situation by naming our table people. ActiveRecord helps us understand much of what is going on in the database, but one piece converts our data into objects. ActiveRecord uses plurals to help describe what a table holds. Just as in English, if we had a group of persons, we would refer to them as people. The same is true with ActiveRecord. We have a table with person data in it; then, when we reference a Person object, ActiveRecord knows it should look in the people table to find information about that Person. The same would be true for a table that stored data about gnomes. The table itself would be called Gnomes, but each object would be a Gnome object. Now that we understand how the table is set up, let's set our class and pull all the records from the database.

```ruby
class Person < ActiveRecord::Base
end
print "methods\n"
Person.each { |p| print "ID: #{p.id} Name: #{p.name}\nHomePage: #{p.homepage}\n" }
```

We create our person class and include the ActiveRecord::Base class. This includes all the default Active Record methods to handle database interaction between our class and the database. Next, we fetch all the records from the database. We use the Person class to fetch all Persons from the People database. We iterate through each record and print it. Notice that our class has already set up our accessors so that we can read and write to these records at will.

Fetching all the information from the table required no knowledge of SQL, and was easily managed by the Ruby conventions which we are familiar. Active Record goes further, giving native methods for querying for specific records as well. The Active Record code autogenerates methods to search based on the fields that were discovered in the database. Let's look at an example.

```ruby
print "\Fetching individual records\n"
ryan = Person.find_by_name('ryan')
print ":ID: #{ryan.id} Name: #{ryan.name} Homepage: #{ryan.homepage}\n"
```

In our code, we use the find_by_name method of the Person class. Ruby autogenerates a find_by method for each field in the database. This lets us search by any of the fields. In this case, we assign the returned record to a variable, and then print out the same way we did with our table dump.

## Tip

Active Record is exceptionally flexible. While we have looked at one way to perform a few different tasks, there are many ways to accomplish each task. The best way to learn about these is to look at the API documentation and experiment. Use the example in this chapter, and try other methods from the API documentation at http://api.rubyonrails.org/classes/ActiveRecord/Base.html.

Now we know how to search for records, let's look at creating a record. We will create our records using a special method in Active Record that allows us to create a record if it doesn't exist, but will retrieve the record if it does. We frequently use this type of method if we have to unique records in our database based on some criteria. Let's look at the code example.

```ruby
ed = Person.where(:name => 'ed', :homepage => 'http://www.counterhack.net').first_or_create
print ":ID: #{ed.id} Name: #{ed.name} Homepage: #{ed.homepage}\n"
```

We use our Person class to search for a record with the name ed if the record needs to be created, we want to create it and assign the homepage as well, so we use the first_or_create method which will either return the first occurrence or create it if it doesn't exist. Next, we store our variable as “ed” and print it.

When we run our code, we can run it multiple times. We will only see one instance of ed. If we wanted a new ed for every execution of our script, we would change our code to use create.
