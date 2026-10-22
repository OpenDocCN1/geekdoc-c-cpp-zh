
## Prices, Dollars, and Cents

When we defined our schema, we decided to store the product price in a decimal column, rather than a float. There was a reason for this. Floating-point numbers are subject to round-off errors: put enough products into your cart, and you might see a total price of 234.99 rather than 235.00. Decimal numbers are stored both in the database and in Ruby as scaled integers, and hence they have exact representations.

But we are not done yet. That takes care of the model only. The flow of control doesn't change, so no changes are needed to the controller. All that is left is the view. Although this does mean that we have to edit four files, the changes are very straightforward. Note that the change is subtly different in the show.html.erb file. Don't worry too much about the details at the moment; we'll revisit the user interface shortly.

```
Download depot_a/app/views/products/index.html.erb
<h1>Listing products</h1>

<table>
  <tr>
    <th>Title</th>
    <th>Description</th>
    <th>Image url</th>
    <th>Price</th>
  </tr>

<% for product in @products %>
  <tr>
    <td><%=h product.title %></td>
    <td><%=h product.description %></td>
    <td><%=h product.image_url %></td>
    <td><%=h product.price %></td>
    <td><%= link_to 'Show', product %></td>
    <td><%= link_to 'Edit', edit_product_path(product) %></td>
    <td><%= link_to 'Destroy', product, :confirm => 'Are you sure?', :method => :delete %></td>
  </tr>
<% end %>
</table>

<br />

<%= link_to 'New product', new_product_path %>
```

```
Download depot_ca/app/views/products/new.html.erb

<h1>New product</h1>

<% form_for(@product) do |f| %>
  <%= f.error_messages %>

  <p>
    <%= f.label :title %><br />
    <%= f.text_field :title %>
  </p>
  <p>
    <%= f.label :description %><br />
    <%= f.text_area :description, :rows => 6 %>
  </p>
  <p>
    <%= f.label :image_url %><br />
    <%= f.text_field :image_url %>
  </p>
  <p>
    <%= f.label :price %><br />
    <%= f.text_field :price %>
  </p>

  <p>
    <%= f.submit "Create" %>
  </p>
<% end %>

<%= link_to 'Back', products_path %>
```

```
Download depot_ca/app/views/products/edit.html.erb

<h1>Editing product</h1>

<% form_for(@product) do |f| %>
  <%= f.error_messages %>

  <p>
    <%= f.label :title %><br />
    <%= f.text_field :title %>
  </p>
  <p>
    <%= f.label :description %><br />
    <%= f.text_area :description %>
  </p>
  <p>
    <%= f.label :image_url %><br />
    <%= f.text_field :image_url %>
  </p>
  <p>
    <%= f.label :price %><br />
    <%= f.text_field :price %>
  </p>
```

```
<p>
  <%= f.submit "Update" %>
</p>
<% end %>

<%= link_to 'Show', @product %> |
<%= link_to 'Back', products_path %>

Download depot_a/app/views/products/show.html.erb

<p>
  <b>Title:</b>
  <%=h @product.title %>
</p>

<p>
  <b>Description:</b>
  <%=h @product.description %>
</p>

<p>
  <b>Image url:</b>
  <%=h @product.image_url %>
</p>

<p>
  <b>Price:</b>
  <%=h @product.price %>
</p>

<%= link_to 'Edit', edit_product_path(@product) %> |
<%= link_to 'Back', products_path %>
```

Here’s the cool part. Go to your browser, which is already talking to the application. Hit Refresh, and you should now see the price column included in these four pages.

We said that the Product model went to the products table to find out what attributes it should have. In development mode, Rails reloads models each time a browser sends in a request, so the model will always reflect the current database schema. And we have updated the views so that they can use this model information to update the screens that are displayed.

There’s no real magic here at the technical level, but this capability has a big impact on the development process. How often have you implemented exactly what a client asked for, only to be told “Oh, that’s not what I meant” when you finally showed them the working application? Most people find it far easier to understand ideas when they can play with them. The speed with which you can turn words into a working application with Rails means that you are never far from being able to let the client play with the results. These short feedback cycles mean that both you and the client get to understand the real requirements sooner, and you waste far less time reworking your application.

![](img/a160fc3a330a0b3b2a764d41d614e688_86_0.png)

# Figure 6.2: The price fails validation.

We make it a protected method, because it shouldn't be called from outside the context of the model. Be careful as you add methods to this model as we work further on the product—if you add them after the protected declaration, they'll be invisible outside the class. New actions must go before the protected line.

protected → page 672

```
validate :price_must_be_at_least_a_cent

protected
def price_must_be_at_least_a_cent
  errors.add(:price, 'should be at least 0.01') if price.nil? || price < 0.01
end
```

The down method empties the table. The migration is created just like any other:

```
depot> ruby script/generate migration add_test_data
exists  db/migrate
create  db/migrate/20080601000003_add_test_data.rb
```

We then add the code to populate the products table. This uses the create method of the Product model. The following is an extract from that file. (Rather than type the migration in by hand, you might want to copy the file from the sample code available online.¹⁵) Copy it to the db/migrate directory in your application, and delete the one you just generated. Don't be concerned if the timestamp of the file you downloaded is before others that you have already migrated, because Rails knows which migrations have been completed and which ones have yet to be done.

While you're there, copy the images¹⁶ and the file depot.css¹⁷ into corresponding places (public/images and public/stylesheets in your application). Be warned: this migration removes existing data from the products table before loading in the new data. You might not want to run it if you've just spent several hours typing your own data into your application!

```
Download depot_c/db/migrate/20080601000003_add_test_data.rb
class AddTestData < ActiveRecord::Migration
  def self.up
    Product.delete_all
    Product.create(:title => 'Pragmatic Version Control',
      :description =>
      %{
        <p>
          This book is a recipe-based approach to using Subversion that will
          get you up and running quickly---and correctly. All projects need
          version control: it's a foundational piece of any project's
          infrastructure. Yet half of all project teams in the U.S. don't use
          any version control at all. Many others don't use it well, and end
          up experiencing time-consuming problems.
        </p>},
      :image_url => '/images/svn.jpg',
      :price => 28.50)
    # ...
  end

  def self.down
    Product.delete_all
  end
end
```

(Note that this code uses %{...}. This is an alternative syntax for double-quoted string literals, convenient for use with long strings. Note also that because

15. http://media.pragprog.com/titles/rails3/code/depot_c/db/migrate/20080601000003_add_test_data.rb
16. http://media.pragprog.com/titles/rails3/code/depot_c/public/images
17. http://media.pragprog.com/titles/rails3/code/depot_c/public/stylesheets/depot.css

it uses Rails' create method, it will fail silently if records cannot be inserted because of validation errors.)

Running the migration will populate your products table with test data:

```
depot>  rake db:migrate
```

Now let's get the product listing tidied up. There are two pieces to this. Eventually we'll be writing some HTML that uses CSS to style the presentation. But for this to work, we'll need to tell the browser to fetch the stylesheet.

We need somewhere to put our CSS style definitions. All scaffold-generated applications use the stylesheet scaffold.css in the directory public/stylesheets. Rather than alter this file, we created a new application stylesheet, depot.css, and put it in the same directory. A full listing of this stylesheet starts on page 721.

Finally, we need to link these stylesheets into our HTML page. If you look at the .html.erb files we've created so far, you won't find any reference to stylesheets. You won't even find the HTML <head> section where such references would normally live. Instead, Rails keeps a separate file that is used to create a standard page environment for all product pages. This file, called products.html.erb, is a Rails layout and lives in the layouts directory:

Download depot_b/app/views/layouts/products.html.erb

```
Line 1 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
5 <head>
  <meta http-equiv="content-type" content="text/html;charset=UTF-8" />
  <title>Products: <%= controller.action_name %></title>
  <%= stylesheet_link_tag 'scaffold' %>
</head>
10 <body>

  <p style="color: green"><%= flash[:notice] %></p>

  <%= yield %>
15
</body>
</html>
```

The eighth line loads the stylesheet. It uses stylesheet_link_tag to create an HTML <link> tag, which loads the standard scaffold stylesheet. We'll simply add our depot.css file here (dropping the .css extension). Don't worry about the rest of the file; we'll look at that later.

Download depot_c/app/views/layouts/products.html.erb

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```
