magic option :encode=>"javascript" uses client-side JavaScript to obscure the generated link, making it harder for spiders to harvest e-mail addresses from your site.⁵

```
<%= mail_to("support@pragprog.com", "Contact Support",
    :subject => "Support question from #{@user.name}",
    :encode => "javascript") %>
```

As a weaker form of obfuscation, you can use the :replace_at and :replace_dot options to replace the at sign and dots in the displayed name with other strings. This is unlikely to fool harvesters.

The AssetTagHelper module also includes helpers that make it easy to link to stylesheets and JavaScript code from your pages and to create autodiscovery Atom feed links. We created a stylesheet link in the layouts for the Depot application, where we used stylesheet_link_tag in the head:

Download depot_r/app/views/layouts/store.html.erb

```
<%= stylesheet_link_tag "depot", :media => "all" %>
```

The stylesheet_include_tag method can also take a parameter named :all indicating that all styles in the stylesheet directory will be included. Adding :recursive => true will cause Rails to include all styles in all subdirectories too.

The javascript_include_tag method takes a list of JavaScript filenames (assumed to live in public/javascripts) and creates the HTML to load these into a page. In addition to :all and :defaults, javascript_include_tag accepts as a parameter the value :defaults, which acts as a shortcut and causes Rails to load the files prototype.js, effects.js, dragdrop.js, and controls.js, along with application.js if it exists. Use the latter file to add your own JavaScript to your application’s pages.⁶

An RSS or Atom link is a header field that points to a URL in our application. When that URL is accessed, the application should return the appropriate RSS or Atom XML:

```
<html>
  <head>
    <%= auto_discovery_link_tag(:atom, :action => 'feed') %>
  </head>
  . . .
```

Finally, the JavaScriptHelper module defines a number of helpers for working with JavaScript. These create JavaScript snippets that run in the browser to generate special effects and to have the page dynamically interact with our

5. But it also means your users won’t see the e-mail link if they have JavaScript disabled in their browsers.

6. Writers of plug-ins can arrange for their own JavaScript files to be loaded when an application specifies :defaults, but that’s beyond the scope of this book.