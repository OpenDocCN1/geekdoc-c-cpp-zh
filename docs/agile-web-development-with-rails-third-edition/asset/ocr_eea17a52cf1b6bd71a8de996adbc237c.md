they've read. That's where the :through option comes in. Let's update our article and user models:

```
class Article < ActiveRecord::Base
  has_many :readings
  has_many :users, :through => :readings
end
```

```
class User < ActiveRecord::Base
  has_many :readings
  has_many :articles, :through => :readings
end
```

The :through option on the two new has_many declarations tells Rails that the readings table can be used to navigate from (say) an article to a number of users who've read that article. Now we can write code such as this:

```
readers = an_article.users
```

Behind the scenes, Rails constructs the necessary SQL to return all the user rows referenced from the readers table where the readers rows reference the original article. (Whew!)

The :through parameter nominates the association to navigate through in the original model class. Thus, when we say this:

```
class Article < ActiveRecord::Base
  has_many :readings
  has_many :users, :through => :readings
end
```

the :through => :readings parameter tells Active Record to use the has_many :readings association to find a model called Reading.

The name we give to the association (:users in this case) then tells Active Record which attribute to use to look up the users (the user_id). You can change this by adding a :source parameter to the has_many declaration. For example, so far we've called the people who have read an article users, simply because that was the name of the association in the Reading model. However, it's easy to call them readers instead—we just have to override the name of the association used:

```
class Article < ActiveRecord::Base
  has_many :readings
  has_many :readers, :through => :readings, :source => :user
end
```

In fact, we can go even further. This is still a has_many declaration, so it will accept all the has_many parameters.