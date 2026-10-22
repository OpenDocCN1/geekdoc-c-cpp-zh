
This code is equivalent to the previous example:

```
article = Article.create(:name => "Join Models")
article.users.create!(:name => "dave")
```

Note that it isn’t possible to set attributes in the intermediate table using this approach.

## Extending Associations

An association declaration (belongs_to, has_xxx) makes a statement about the business relationship between your model objects. Quite often, additional business logic is associated with that particular association. In the previous example, we defined a relationship between articles and their readers called Reading. This relationship incorporated the user’s rating of the article they’d just read. Given a user, how can we get a list of all the articles they’ve rated with three stars or higher? Four or higher?

We’ve already seen one way: we can construct new associations where the result set meets some additional criteria. We did that with the happy_users association on the previous page. However, this method is constrained—we can’t parameterize the query, letting our caller determine the rating that counts as being “happy.”

An alternative is to have the code that uses our model add additional conditions on the query itself:

```
user = User.find(some_id)
user.articles.find(:all, :conditions => [ 'rating >= ?', 3])
```

This works but gently breaks encapsulation: we’d really like to keep the idea of finding articles based on their rating wrapped inside the articles association. Rails lets us do this by adding a block to any has_many declaration. Any methods defined in this block become methods of the association.

The following code adds the finder method rated_at_or_above to the articles association in the user model:

```
class User < ActiveRecord::Base
  has_many :readings
  has_many :articles, :through => :readings do
    def rated_at_or_above(rating)
      find :all, :conditions => ['rating >= ?', rating]
    end
  end
end
```

Given a user model object, we can now call this method to retrieve a list of the articles they’ve rated highly:

```
user = User.find(some_id)
good_articles = user.articles.rated_at_or_above(4)
```

into a single database table. This table contains a column for each of the attributes of all the classes in the hierarchy. It additionally includes a column, by convention called type, that identifies which particular class of object is represented by any particular row. This is illustrated in Figure 19.2, on the following page.

Using single-table inheritance in Active Record is straightforward. Define the inheritance hierarchy you need in your model classes, and ensure that the table corresponding to the base class of the hierarchy contains a column for each of the attributes of all the classes in that hierarchy. The table must additionally include a type column, used to discriminate the class of the corresponding model objects.

When defining the table, remember that the attributes of subclasses will be present only in the table rows corresponding to those subclasses; an employee doesn't have a balance attribute, for example. As a result, you must define the table to allow null values for any column that doesn't appear in all subclasses. The following is the migration that creates the table illustrated in Figure 19.2, on the next page:

```
create_table :people, :force => true do |t|
  t.string :type

  # common attributes
  t.string :name
  t.string :email

  # attributes for type=Customer
  t.decimal :balance, :precision => 10, :scale => 2

  # attributes for type=Employee
  t.integer :reports_to
  t.integer :dept

  # attributes for type=Manager
  # -- none --
end
```

We can define our hierarchy of model objects:

```
class Person < ActiveRecord::Base
end

class Customer < Person
end

class Employee < Person
  belongs_to :boss, :class_name => "Manager", :foreign_key => :reports_to
end
```

```
Customer.create(:name => 'Bert Public', :email => "b@public.net", :balance => 12.45)

barney = Employee.new(:name => 'Barney Rub', :email => "barney@here.com", :dept => 23)

barney.boss = wilma
barney.save!
```

```
manager = Person.find_by_name("Wilma Flint")
puts manager.class      #=> Manager
puts manager.email      #=> wilma@here.com
puts manager.dept       #=> 23
```

```
customer = Person.find_by_name("Bert Public")
puts customer.class    #=> Customer
puts customer.email    #=> b@public.net
puts customer.balance  #=> 12.45
```

Notice how we ask the base class, Person, to find a row, but the class of the object returned is Manager in one instance and Customer in the next; Active Record determined the type by examining the type column of the row and created the appropriate object.

Notice also a small trick we used in the Employee class. We used belongs_to to create an attribute named boss. This attribute uses the reports_to column, which points back into the people table. That’s what lets us say barney.boss = wilma.

There’s one fairly obvious constraint when using single-table inheritance. Two subclasses can’t have attributes with the same name but with different types, because the two attributes would map to the same column in the underlying schema.

There’s also a less obvious constraint. The attribute type is also the name of a built-in Ruby method, so accessing it directly to set or change the type of a row may result in strange Ruby messages. Instead, access it implicitly by creating objects of the appropriate class, or access it via the model object’s indexing interface, using something such as this:

```
person[:type] = 'Manager'
```

## Polymorphic Associations

One major downside of STI is that there’s a single underlying table that contains all the attributes for all the subclasses in our inheritance tree. We can overcome this using Rails’ second form of heterogeneous aggregation, polymorphic associations.

## Joe Asks...

## What If We Want Straight Inheritance?

Single-table inheritance is clever—it turns on automatically whenever we subclass an Active Record class. But what if we want real inheritance? What if we want to define some behavior to be shared among a set of Active Record classes by defining an abstract base class and a set of subclasses?

The answer is to define a class method called abstract_class? in our abstract base class. The method should return true. This has two effects. First, Active Record will never try to find a database table corresponding to this abstract class. Second, all subclasses of this class will be treated as independent Active Record classes—each will map to its own database table.

Of course, a better way of doing this is probably to use a Ruby module containing the shared functionality and mix this module into Active Record classes that need that behavior.

Polymorphic associations rely on the fact that a foreign key column is simply an integer. Although there’s a convention that a foreign key named user_id references the id column in the users table, there’s no law that enforces this.³

In computer science, polymorphism is a mechanism that lets you abstract the essence of something’s interface regardless of its underlying implementation. The addition method, for example, is polymorphic, because it works with integers, floats, and even strings.

In Rails, a polymorphic association is an association that links to objects of different types. The assumption is that these objects all share some common characteristics but that they’ll have different representations.

To make this concrete, let’s look at a simple asset management system. We index our assets in a simple catalog. Each catalog entry contains a name, the acquisition date, and a reference to the actual resource: an article, an image, a sound, and so on. Each of the different resource types corresponds to a different database table and to a different Active Record model, but they are all assets, and they are all cataloged.

3. If you specify that your database should enforce foreign key constraints, polymorphic associations won’t work.
