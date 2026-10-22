Rather than clutter the products table, we'll keep it in an ancillary details table:

```
class CreateDetails < ActiveRecord::Migration
  def self.up
    create_table :details do |t|
      t.integer :product_id
      t.string :sku
      t.string :manufacturer
    end
  end

  def self.down
    drop_table :details
  end
end
```

The model is equally trivial:

```
class Detail < ActiveRecord::Base
  belongs_to :product
  validates_presence_of :sku
end
```

The view uses form_for to capture the fields for the product model and uses a fields_for call within that form to capture the details model data:

```
<% form_for :product, :url => { :action => :create } do |form| %>
  <%= error_messages_for :product %>
  Title: <%= form.text_field :title %><br/>
  Description: <%= form.text_area :description, :rows => 3 %><br/>
  Image url: <%=form.text_field :image_url %><br/>

  <fieldset>
    <legend>Details...</legend>
    <%= error_messages_for :details %>
    <% fields_for :details do |detail| %>
      SKU: <%= detail.text_field :sku %><br/>
      Manufacturer: <%= detail.text_field :manufacturer %>
    <% end %>
  </fieldset>
  <%= submit_tag %>
<% end %>
```

We can look at the generated HTML to see this in action:

```
<form action="/products/create" method="post">
  Title:
  <input id="product_title" name="product[title]" size="30" type="text" /><br/>
  Description:
  <textarea cols="40" id="product_description"
    name="product[description]" rows="3"></textarea><br/>
```