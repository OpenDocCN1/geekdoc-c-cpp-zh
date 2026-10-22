
## What’s with :method => :delete?

You may have noticed that the scaffold-generated *destroy* link includes the parameter :method => :delete. This parameter was added to Rails 1.2. This determines which method is called in the ProductsController class and also affects which HTTP method is used.

Browsers use HTTP to talk with servers. HTTP defines a set of verbs that browsers can employ and defines when each can be used. A regular hyperlink, for example, uses an HTTP GET request. A GET request is defined by HTTP to be used to retrieve data; it isn’t supposed to have any side effects. So, the Rails team changed the scaffold code generator to force the link to issue an HTTP DELETE*. These DELETE requests are permitted to have side effects and so are more suitable for deleting resources.

* In some cases, Rails will substitute the POST HTTP method for DELETE, based on whether the browser is capable of issuing a DELETE method. Either way, the request will not be cached or triggered by web crawlers.

Even this simple template uses a number of built-in Rails features:

- The rows in the listing have alternating background colors. This is done by setting the CSS class of each row to either list-line-even or list-line-odd. The Rails helper method called cycle does this, automatically toggling between the two style names on successive lines.
- The truncate helper is used to display just the first eighty characters of the description. But before we call truncate, we called gsub in order to remove the HTML tags from the description.¹⁸
- We also used the h method to ensure that any remaining HTML in the product title and description is escaped.
- Look at the link_to ’Destroy’ line. See how it has the parameter :confirm => "Are you sure?". If you click this link, Rails arranges for your browser to pop up a dialog box asking for confirmation before following the link and deleting the product. (Also, see the sidebar on this page for some scoop on this action.)

We loaded some test data into the database, we rewrote the index.html.erb file that displays the listing of products, we added a depot.css stylesheet, and we linked that stylesheet into our page by editing the layout file products.html.erb.

18. If you get a message such as undefined method `for' for {length=>80}.Hash, then you probably aren’t running Rails 2.2.2 or later. See Chapter 3, *Installing Rails*, on page 31 for upgrade information, or simply remove length => from this call (leaving the 80).

In this chapter, we’ll see

- writing our own views,
- using layouts to decorate pages,
- integrating CSS,
- using helpers, and
- linking pages to actions.

## Chapter 7

## Task B: Catalog Display

All in all, it’s been a successful day so far. We gathered the initial requirements from our customer, documented a basic flow, worked out a first pass at the data we’ll need, and put together the maintenance page for the Depot application’s products. We even managed to cap off the morning with a decent lunch.

Thus fortified, it’s on to our second task. We chatted about priorities with our customer, and she said she’d like to start seeing what the application looks like from the buyer’s point of view. Our next task is to create a simple catalog display.

This also makes a lot of sense from our point of view. Once we have the products safely tucked into the database, it should be fairly simple to display them. It also gives us a basis from which to develop the shopping cart portion of the code later.

We should also be able to draw on the work we just did in the product maintenance task—the catalog display is really just a glorified product listing. So, let’s get started.

### 7.1 Iteration B1: Creating the Catalog Listing

We’ve already created the products controller, used by the seller to administer the Depot application. Now it’s time to create a second controller, one that interacts with the paying customers. Let’s call it Store.

```
depot> ruby script/generate controller store index
exists   app/controllers/
exists   app/helpers/
create   app/views/store
exists   test/functional/
create   app/controllers/store_controller.rb
create   test/functional/store_controller_test.rb
create   app/helpers/store_helper.rb
create   app/views/store/index.html.erb
```

![](img/a160fc3a330a0b3b2a764d41d614e688_97_0.png)

Figure 7.1: Our first (ugly) catalog page

In general, try to get into the habit of typing <%=h ... %> in templates and then removing the h only when you’ve convinced yourself it’s safe to do so.

We’ve also used the image_tag helper method. This generates an HTML <img> tag using its argument as the image source.

Hitting Refresh brings up the display in Figure 7.1. It’s pretty ugly, because we haven’t yet included the CSS stylesheet. The customer happens to be walking by as we ponder this, and she points out that she’d also like to see a decent-looking title and sidebar on public-facing pages.

At this point in the real world, we’d probably want to call in the design folks—we’ve all seen too many programmer-designed websites to feel comfortable inflicting another on the world. But Pragmatic Web Designer is off getting inspiration on a beach somewhere and won’t be back until later in the year, so let’s put a placeholder in for now. It’s time for an iteration.

### 7.2 Iteration B2: Adding a Page Layout

The pages in a typical website often share a similar layout—the designer will have created a standard template that is used when placing content. Our job is to add this page decoration to each of the store pages.

Fortunately, in Rails we can define layouts. A layout is a template into which we can flow additional content. In our case, we can define a single layout for all the store pages and insert the catalog page into that layout. Later we can do the same with the shopping cart and checkout pages. Because there's only one layout, we can change the look and feel of this entire section of our site by editing just one file. This makes us feel better about putting a placeholder in for now; we can update it when the designer eventually returns from the islands.

There are many ways of specifying and using layouts in Rails. We'll choose the simplest for now. If we create a template file in the app/views/layouts directory with the same name as a controller, all views rendered by that controller will use that layout by default. So, let's create one now. Our controller is called store, so we'll name the layout store.html.erb:

Download depot_e/app/views/layouts/store.html.erb

```
Line 1 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html>
<head>
<title>Pragprog Books Online Store</title>
<%= stylesheet_link_tag "depot", :media => "all" %>
</head>
<body id="store">
<div id="banner">
<%= image_tag("logo.png") %>
<%= @page_title || "Pragmatic Bookshelf" %>
</div>
<div id="columns">
<div id="side">
<a href="http://www....">Home</a><br />
<a href="http://www..../faq">Questions</a><br />
<a href="http://www..../news">News</a><br />
<a href="http://www..../contact">Contact</a><br />
</div>
<div id="main">
<%= yield :layout %>
</div>
</div>
</body>
</html>
```

Apart from the usual HTML gubbins, this layout has three Rails-specific items. Line 6 uses a Rails helper method to generate a <link> tag to our depot.css

stylesheet. On line 11, we set the page heading to the value in the instance variable @page_title. The real magic, however, takes place on line 21. When we invoke yield, passing it the name :layout, Rails automatically substitutes in the page-specific content—the stuff generated by the view invoked by this request. In our case, this will be the catalog page generated by index.html.erb.³

To make this all work, we need to add the following to our depot.css stylesheet:

```
Download depot_e/public/stylesheets/depot.css

/* Styles for main page */

#banner {
  background: #9c9;
  padding-top: 10px;
  padding-bottom: 10px;
  border-bottom: 2px solid;
  font: small-caps 40px/40px "Times New Roman", serif;
  color: #282;
  text-align: center;
}

#banner img {
  float: left;
}

#columns {
  background: #141;
}

#main {
  margin-left: 13em;
  padding-top: 4ex;
  padding-left: 2em;
  background: white;
}

#side {
  float: left;
  padding-top: 1em;
  padding-left: 1em;
  padding-bottom: 1em;
  width: 12em;
  background: #141;
}

#side a {
  color: #bfb;
  font-size: small;
}
```

3. Rails also sets the variable @content_for_layout to the results of rendering the action, so you can also substitute this value into the layout in place of the yield. This was the original way of doing it (and we personally find it more readable). Using yield is considered sexier.
