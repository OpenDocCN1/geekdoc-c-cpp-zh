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