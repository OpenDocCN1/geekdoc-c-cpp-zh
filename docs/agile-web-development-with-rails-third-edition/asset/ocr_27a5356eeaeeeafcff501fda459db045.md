# Using Models as Join Tables

Current Rails thinking is to keep join tables pure—a join table should contain only a pair of foreign key columns. Whenever you feel the need to add more data to this kind of table, what you're really doing is creating a new model, because the join table changes from a simple linkage mechanism into a fully fledged participant in the business of your application. Let's look back at the previous example with articles and users.

In the simple “habtm” implementation, the join table records the fact that an article was read by a user. Rows in the join table have no independent existence. But pretty soon we find ourselves wanting to add information to this table. We want to record when the reader read the article and how many stars they gave it when finished. The join table suddenly has a life of its own and deserves its own Active Record model. Let's call it Reading. The schema looks like this:

![](bbox=[0.18, 0.35, 0.78, 0.48])

Using the Rails facilities we've seen so far in this chapter, we could model this using the following:

```
class Article < ActiveRecord::Base
  has_many :readings
end
```

```
class User < ActiveRecord::Base
  has_many :readings
end
```

```
class Reading < ActiveRecord::Base
  belongs_to :article
  belongs_to :user
end
```

When a user reads an article, we can record that fact:

```
reading = Reading.new
reading.rating  = params[:rating]
reading.read_at = Time.now
reading.article = current_article
reading.user    = session[:user]
reading.save
```

However, we've lost something compared to the “habtm” solution. We can no longer easily ask an article who its readers are or ask a user which articles