
![](img/a160fc3a330a0b3b2a764d41d614e688_390_0.png)

| categories |
| id | parent_id | rest_of_data |
| 1 | null | ... |
| 2 | 1 | ... |
| 3 | 1 | ... |
| 4 | 3 | ... |
| 5 | 1 | ... |
| 6 | 3 | ... |
| 7 | 2 | ... |
| 8 | 6 | ... |
| 9 | 6 | ... |

## Figure 19.4: Representing a tree using parent links in a table

```
Download e1/ar/acts_as_tree.rb
create_table :categories, :force => true do |t|
  t.string :name
  t.integer :parent_id
end
```

The corresponding model uses the method with the tribal name acts_as_tree to specify the relationship. The :order parameter means that when we look at the children of a particular node, we'll see them arranged by their name column:

```
Download e1/ar/acts_as_tree.rb
class Category < ActiveRecord::Base
  acts_as_tree :order => "name"
end
```

Normally you'd have some end-user functionality to create and maintain the category hierarchy. Here, we'll just create it using code. Note how we manipulate the children of any node using the children attribute:

```
Download e1/ar/acts_as_tree.rb
root        = Category.create(:name => "Books")
fiction     = root.children.create(:name => "Fiction")
non_fiction = root.children.create(:name => "Non Fiction")

non_fiction.children.create(:name => "Computers")
non_fiction.children.create(:name => "Science")
non_fiction.children.create(:name => "Art History")

fiction.children.create(:name => "Mystery")
fiction.children.create(:name => "Romance")
fiction.children.create(:name => "Science Fiction")
```

## David Says. . .

## Why Things in Associations Get Saved When They Do

It might seem inconsistent that assigning an order to the invoice will not save the association immediately, but the reverse will. This is because the invoices table is the only one that holds the information about the relationship. Hence, when you associate orders and invoices, it’s always the invoice rows that hold the information. When you assign an order to an invoice, you can easily make this part of a larger update to the invoice row that might also include the billing date. It’s therefore possible to fold what would otherwise have been two database updates into one. In an ORM, it’s generally the rule that fewer database calls is better.

When an order object has an invoice assigned to it, it still needs to update the invoice row. So, there’s no additional benefit in postponing that association until the order is saved. In fact, it would take considerably more software to do so. And Rails is all about less software.

the invoice that it’s associated with an order. The two are almost equivalent. The difference is in the way they save (or don’t save) objects to the database. If you assign an object to a has_one association in an existing object, that associated object will be automatically saved:

```
order = Order.find(some_id)
an_invoice = Invoice.new(...)
order.invoice = an_invoice      # invoice gets saved
```

If instead you assign a new object to a belongs_to association, it will never be automatically saved:

```
order = Order.new(...)      # Order will not be saved here
an_invoice.order = order    # both the invoice and the order get saved
an_invoice.save
```

Finally, there’s a danger here. If the child row cannot be saved (for example, because it fails validation), Active Record will not complain—you’ll get no indication that the row was not added to the database. For this reason, we strongly recommend that instead of the previous code, you write this:

```
invoice = Invoice.new
# fill in the invoice
invoice.save!
an_order.invoice = invoice
```

The save! method throws an exception on failure, so at least you’ll know that something went wrong.

And this example will bring it all down to as few queries, possibly even to the point of doing all the work in a single query:

```
for post in Post.find(:all, :include => [:author, :comments])
  puts "Post:           #{post.title}"
  puts "Written by:     #{post.author.name}"
  puts "Last comment on: #{post.comments.first.created_on}"
end
```

This preloading is not guaranteed to improve performance.⁵ And even if the optimization does work, the query can end up returning a lot of data to be converted into Active Record objects. If your application doesn’t use the extra information, you’ve incurred a cost for no benefit. You might also have problems if the parent table contains a large number of rows—compared with the row-by-row lazy loading of data, the preloading technique will consume a lot more server memory.

If you use :include, you’ll need to disambiguate all column names used in other parameters to find—prefix each with the name of the table that contains it. In the following example, the title column in the condition needs the table name prefix for the query to succeed:

```
for post in Post.find(:all, :conditions => "posts.title like '%ruby%'",
                     :include => [:author, :comments])
  # ...
end
```

## 19.9 Counters

The has_many relationship defines an attribute that is a collection. It seems reasonable to be able to ask for the size of this collection: how many line items does this order have? And indeed you’ll find that the aggregation has a size method that returns the number of objects in the association. This method goes to the database and performs a select count(*) on the child table, counting the number of rows where the foreign key references the parent table row.

This works and is reliable. However, if you’re writing a site where you frequently need to know the counts of child items, this extra SQL might be an overhead you’d rather avoid. Active Record can help using a technique called counter caching. In the belongs_to declaration in the child model we can ask Active Record to maintain a count of the number of associated children in the parent table rows. This count will be automatically maintained—if we add a child row, the count in the parent row will be incremented, and if we delete a child row, it will be decremented.

5. In fact, it might not work at all! If your database doesn’t support left outer joins, you can’t use the feature. Oracle 8 users, for instance, will need to upgrade to version 9 to use preloading.

## Chapter 20

## Active Record Part III:
Object Life Cycle

So far we've looked at how to connect to Active Record, access data and attributes, and link together tables. This chapter rounds off our description of Active Record. It looks at the life cycle of Active Record objects; the validations and hooks that you can define affect how they are processed.

## 20.1 Validation

Active Record can validate the contents of a model object. This validation can be performed automatically when an object is saved. You can also programmatically request validation of the current state of a model. If validation fails when you're saving an object, the object will not be written to the database; it will be left in memory in its invalid state. This allows you (for example) to pass the object back to a form so the user can correct the bad data.

Active Record distinguishes between models that correspond to an existing row in the database and those that don't. The latter are called new records (the new_record? method will return true for them). When you call the save method, Active Record will perform a SQL insert operation for new records and an update for existing ones.

This distinction is reflected in Active Record's validation workflow—you can specify validations that are performed on all save operations and other validations that are performed only on creates or updates.

At the lowest level you specify validations by listing one or more methods names as symbols on calls to the validate, validate_on_create, and validate_on_update class methods. validate methods are invoked on every save operation.

One of the other two is invoked depending on whether the record is new or whether it was previously read from the database.

You can also run validation at any time without saving the model object to the database by calling the valid? method. This invokes the same two validation methods that would be invoked if save had been called.

For example, the following code ensures that the username column is always set to something valid and that the name is unique for new User objects. (We’ll see later how these types of constraints can be specified more simply.)

```
class User < ActiveRecord::Base
  validate :valid_name?
  validate_on_create :unique_name?

private

  def valid_name?
    unless name && name =~ /^\w+$/
      errors.add(:name, "is missing or invalid")
    end
  end

  def unique_name?
    if User.find_by_name(name)
      errors.add(:name, "is already being used")
    end
  end
end
```

When a validate method finds a problem, it adds a message to the list of errors for this model object using errors.add. The first parameter is the name of the offending attribute, and the second is an error message. If you need to add an error message that applies to the model object as a whole, use the add_to_base method instead. (Note that this code uses the support method blank?, which returns true if its receiver is nil or an empty string.)

```
def one_of_name_or_email_required
  if name.blank? && email.blank?
    errors.add_to_base("You must specify a name or an email address")
  end
end
```

As we’ll see on page 536, Rails views can use this list of errors when displaying forms to end users—the fields that have errors will be automatically highlighted, and it’s easy to add a pretty box with an error list to the top of the form.

You can get the errors for a particular attribute using errors.on(:name) (aliased to errors[:name]), and you can clear the full list of errors using errors.clear. If you
