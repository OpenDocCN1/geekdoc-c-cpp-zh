# Field Helpers and form_for

form_for takes a block (the code between it and the <% end %>). It passes this block a form builder object. Inside the block we can use all the normal mixture of HTML and ERb available anywhere in a template. But, we can also use the form builder object to add form elements. As an example, here’s a simple form that captures new product information:

```
Download e1/views/app/views/form_for/new.html.erb
<% form_for :product, :url => { :action => :create } do |form| %>
<p>Title:     <%= form.text_field :title, :size => 30 %></p>
<p>Description: <%= form.text_area :description, :rows => 3 %></p>
<p>Image URL:  <%= form.text_field :image_url %></p>
<p>Price:      <%= form.text_field :price, :size => 10 %></p>
<%= form.select :title, %w{ one two three } %>
<p><%= submit_tag %></p>
<% end %>
```

The significant thing here is the use of form builder helpers to construct the HTML <input> tags on the form. When we create a template containing something like this:

```
<% form_for :product, :url => { :action => :create } do |form| %>
  <p>
    Title:     <%= form.text_field :title, :size => 30 %>
  </p>
<% end %>
```

Rails will generate HTML like this:

```
<form action="/form_for/create" method="post">
  <p>
    Title: <input id="product_title" name="product[title]"
                   size="30" type="text" />
  </p>
```

Notice how Rails has automatically named the input field after both the name of the model object (product) and the name of the field (title).

Rails provides helper support for text fields (regular, hidden, password, and text areas), radio buttons, and checkboxes. (It also supports <input> tags with type="file", but we’ll discuss these in Section 23.8, Uploading Files to Rails Applications, on page 544.)

All form builder helper methods take at least one parameter: the name of the attribute in the model to be queried when setting the field value. When we say this:

```
<% form_for :product, :url => { :action => :create } do |form| %>
  <p>
    Title:     <%= form.text_field :title, :size => 30 %>
  </p>
<% end %>
```

Rails will populate the <input> tag with the value from @product.title. The name parameter may be a string or a symbol; idiomatic Rails uses symbols.