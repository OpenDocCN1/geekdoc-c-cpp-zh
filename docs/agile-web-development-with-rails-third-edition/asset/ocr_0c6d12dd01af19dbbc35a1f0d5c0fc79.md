# :offset

The :offset parameter goes hand in hand with the :limit parameter. It allows us to specify the offset of the first row in the result set that will be returned by find.

```
# The view wants to display orders grouped into pages,
# where each page shows page_size orders at a time.
# This method returns the orders on page page_num (starting
# at zero).
def Order.find_on_page(page_num, page_size)
  find(:all,
    :order => "id",
    :limit => page_size,
    :offset => page_num*page_size)
end
```

We can use :offset in conjunction with :limit to step through the results of a query n rows at a time.

# :joins

The :joins parameter to the finder method lets us specify a list of additional tables to be joined to the default table. This parameter is inserted into the SQL immediately after the name of the model's table and before any conditions specified by the first parameter. The join syntax is database-specific. The following code returns a list of all line items for the book called Programming Ruby:

```
LineItem.find(:all,
  :conditions => "pr.title = 'Programming Ruby'",
  :joins      => "as li inner join products as pr on li.product_id = pr.id")
```

In addition to being able to specify :joins as a string, we can pass a symbol, an array, or a hash, and Rails will build the SQL query for us. For details, see the documentation for ActiveRecord::Associations::ClassMethods under Table Aliasing.

As we'll see in Chapter 19, Active Record: Relationships Between Tables, on page 357, we probably won't use the :joins parameter of find very much—Active Record handles most of the common intertable joins for us.

# :select

By default, find fetches all the columns from the underlying database table—it issues a select * from... to the database. Override this with the :select option, which takes a string that will appear in place of the * in the select statement.

This option allows us to limit the values returned in cases where we need only a subset of the data in a table. For example, our table of podcasts might contain information on the title, speaker, and date and might also contain a