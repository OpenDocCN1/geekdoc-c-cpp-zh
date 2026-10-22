
## Action Controller: Routing and URLs

Action Pack lies at the heart of Rails applications. It consists of two Ruby modules, ActionController and ActionView. Together, they provide support for processing incoming requests and generating outgoing responses. In this chapter and the next, we'll look at ActionController and how it works within Rails. In the chapter that follows these two, we'll take on ActionView.

When we looked at Active Record, we treated it as a freestanding library; you can use Active Record as a part of a nonweb Ruby application. Action Pack is different. Although it is possible to use it directly as a framework, you probably won't. Instead, you'll take advantage of the tight integration offered by Rails. Components such as Action Controller, Action View, and Active Record handle the processing of requests, and the Rails environment knits them together into a coherent (and easy-to-use) whole. For that reason, we'll describe Action Controller in the context of Rails. Let's start by looking at how Rails applications handle requests. We'll then dive down into the details of routing and URL handling. Chapter 22, Action Controller and Rails, then looks at how you write code in a controller.

### 21.1 The Basics

At its simplest, a web application accepts an incoming request from a browser, processes it, and sends a response.

The first question that springs to mind is, how does the application know what to do with the incoming request? A shopping cart application will receive requests to display a catalog, add items to a cart, check out, and so on. How does it route these requests to the appropriate code?

It turns out that Rails provides two ways to define how to route a request: a comprehensive way that you will use when you need to and a convenient way that you will generally use whenever you can.

The rails command generates the initial set of files for an application. One of these files is config/routes.rb. It contains the routing information for that application. If you look at the default contents of the file, ignoring comments, you'll see the following:

```
ActionController::Routing::Routes.draw do |map|
  map.connect ':controller/:action/:id'
  map.connect ':controller/:action/:id.:format'
end
```

The Routing component draws a map that lets Rails connect external URLs to the internals of the application. Each map.connect declaration specifies a route connecting external URLs and internal program code. Let's look at the first map.connect line. The string ':controller/:action/:id' acts as a pattern, matching against the path portion of the request URL. In this case, the pattern will match any URL containing three components in the path. (This isn't actually true, but we'll clear that up in a minute.) The first component will be assigned to the parameter :controller, the second to :action, and the third to :id. Feed this pattern the URL with the path store/add_to_cart/123, and you'll end up with these parameters:

```
@params = { :controller => 'store',
             :action    => 'add_to_cart',
             :id        => 123 }
```

Based on this, Rails will invoke the add_to_cart method in the store controller. The :id parameter will have a value of 123.

### Playing with Routes

Initially, routes can be somewhat intimidating. As you start to define more and more complex routes, you'll start to encounter a problem—how do you know that your routes work the way you expect?

Clearly, one approach is to fire up your application and enter URLs into a browser. However, we can do better than that. For ad hoc experimentation with routes, we can use the script/console command. (For more formal verification we can write unit tests, as we'll see starting on page 458.) We're going to look at how to play with routes now, because it'll come in handy when we look at all the features of routing later.

The routing definition for an application is loaded into a RouteSet object in the ActionController::Routing module. Somewhat confusingly, we can access this via the Routes constant (which turns out not to be that constant). In particular, we can get to the routing definition using script/console, which lets us play with them interactively.

```
>> rs.generate :controller => :store
=> "/store"
>> rs.generate :controller => :store, :id => 123
=> "/store/index/123"
```

All of these examples used our application’s routing and relied on our application having implemented all the controllers referenced in the request path—routing checks that the controller is valid and so won’t parse a request for a controller it can’t find. For example, our Depot application doesn’t have a coupon controller. If we try to parse an incoming route that uses this controller, the path won’t be recognized:

```
>> rs.recognize_path "/coupon/show/1"
ActionController::RoutingError: no route found to match
"/coupon/show/1" with {}
```

We can tell routing to pretend that our application contains controllers that have not yet been written with the use_controllers! method:

```
>> ActionController::Routing.use_controllers! ["store", "admin", "coupon"]
=> ["store", "admin", "coupon"]
```

However, for this change to take effect, we need to reload the definition of the routes:

```
>> load "config/routes.rb"
=> true
>> rs.recognize_path "/coupon/show/1"
=> {:action=>"show", :controller=>"coupon", :id=>"1"}
```

We can use this trick to test routing schemes that are not yet part of our application: create a new Ruby source file containing the Routes.draw block that would normally be in the routes.rb configuration file, and load this new file using load.

### Defining Routes with map.connect

The patterns accepted by map.connect are simple but powerful:

- Components are separated by forward slash characters and periods. Each component in the pattern matches one or more components in the URL. Components in the pattern match in order against the URL.
- A pattern component of the form :name sets the parameter name to whatever value is in the corresponding position in the URL.
- A pattern component of the form *name accepts all remaining components in the incoming URL. The parameter name will reference an array containing their values. Because it swallows all remaining components of the URL, *name must appear at the end of the pattern.

link_to to generate route-based URLs. The only reason we’re using the generate method here is that it works in the context of a console session.

In the following example, Rails will invoke the display_checkout_form action when it receives a GET request to /store/checkout, but it will call the action save_checkout_form if it sees a POST request to that same URL:

```
Download e1/routing/config/routes_with_conditions.rb
ActionController::Routing::Routes.draw do |map|
  map.connect 'store/checkout',
    :conditions => { :method => :get },
    :controller => "store",
    :action     => "display_checkout_form"

  map.connect 'store/checkout',
    :conditions => { :method => :post },
    :controller => "store",
    :action     => "save_checkout_form"
end
```

:name => value

Sets a default value for the component :name. Unlike the values set using :defaults, the name need not appear in the pattern itself. This allows you to add arbitrary parameter values to incoming requests. The value will typically be a string or nil.

:name => /regexp/

Equivalent to using requirements to set a constraint on the value of :name.

There’s one more rule: routing tries to match an incoming URL against each rule in routes.rb in turn. The first match that succeeds is used. If no match succeeds, an error is raised.

Now let’s look at a more complex example. In your blog application, you’d like all URLs to start with the word blog. If no additional parameters are given, you’ll display an index page. If the URL looks like blog/show/nnn, you’ll display article nnn. If the URL contains a date (which may be year, year/month, or year/month/day), you’ll display articles for that date. Otherwise, the URL will contain a controller and action name, allowing you to edit articles and otherwise administer the blog. Finally, if you receive an unrecognized URL pattern, you’ll handle that with a special action.

The routing for this contains a line for each individual case:

```
Download e1/routing/config/routes_for_blog.rb
ActionController::Routing::Routes.draw do |map|
  # Straight 'http://my.app/blog/' displays the index
  map.connect "blog/",
    :controller => "blog",
    :action => "index"
```
