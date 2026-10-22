in the underlying line_items table. belongs_to takes a number of other options, and we'll look at these when we cover more advanced topics.

The belongs_to method creates a number of instance methods for managing the association. The names of these methods all include the name of the association. Let's look at the LineItem class:

```
class LineItem < ActiveRecord::Base
  belongs_to :product
end
```

In this case, the following methods will be defined for line items and for the products to which they belong:

product(force_reload=false)
Returns the associated product (or nil if no associated product exists). The result is cached, and the database will not be queried again when this association is subsequently used unless true is passed as a parameter.

Most commonly this method is called as if it were a simple attribute of (say) a line item object:

```
li = LineItem.find(1)
puts "The product name is #{li.product.name}"
```

product=obj
Associates this line item with the given product, setting the product_id column in this line item to the product's primary key. If the product has not been saved, it will be when the line item is saved, and the keys will be linked at that time.

build_product(attributes={})
Constructs a new product object, initialized using the given attributes. This line item will be linked to it. The product will not yet have been saved.

create_product(attributes={})
Builds a new product object, links this line item to it, and saves the product.

Let's see some of these automatically created methods in use. We have the following models:

```
class Product < ActiveRecord::Base
  has_many :line_items
end
```

```
class LineItem < ActiveRecord::Base
  belongs_to :product
end
```