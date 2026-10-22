Next we'll create the model classes. Note that in the Parent class, we order our children based on the value in the position column. This ensures that the array fetched from the database is in the correct list order.

```
class Parent < ActiveRecord::Base
  has_many :children, :order => :position
end

class Child < ActiveRecord::Base
  belongs_to :parent
  acts_as_list :scope => :parent
end
```

In the Child class, we have the conventional belongs_to declaration, establishing the connection with the parent. We also have an acts_as_list declaration. We qualify this with a :scope option, specifying that the list is per parent record. Without this scope operator, there'd be one global list for all the entries in the children table.

Now we can set up some test data: we'll create four children for a particular parent, calling them One, Two, Three, and Four:

```
parent = Parent.create
%w{ One Two Three Four}.each do |name|
  parent.children.create(:name => name)
end
parent.save
```

We'll write a method to let us examine the contents of the list. There's a subtlety here—notice that we pass true to the children association. That forces it to be reloaded every time we access it. That's because the various move_ methods update the child items in the database, but because they operate on the children directly, the parent will not know about the change immediately. The reload forces them to be brought into memory.

```
def display_children(parent)
  puts parent.children(true).map {|child| child.name }.join(", ")
end
```

And finally we'll play around with our list. The comments show the output produced by display_children:

```
display_children(parent)      #=> One, Two, Three, Four

puts parent.children[0].first?   #=> true
```