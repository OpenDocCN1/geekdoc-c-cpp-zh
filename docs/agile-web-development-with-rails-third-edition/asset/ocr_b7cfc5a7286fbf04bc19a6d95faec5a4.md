show
Returns the contents of the resource identified by params[:id].

update
Updates the contents of the resource identified by params[:id] with the data associated with the request.

edit
Returns the contents of the resource identified by params[:id] in a form suitable for editing.

destroy
Destroys the resource identified by params[:id].

You can see that these seven actions contain the four basic CRUD operations (create, read, update, and delete). They also contain an action to list resources and two auxiliary actions that return new and existing resources in a form suitable for editing on the client.

If for some reason you don’t need or want all seven actions, you can limit the actions produced using :only or :except options on your map.resource:

```
map.resources :comments, :except => [:update, :destroy]
```

Several of the routes are named routes—as described in Section 21.2, Named Routes, on page 438—enabling you to use helper functions such as articles_url and edit_article_url(:id=>1). Two routes are defined for each controller action: one with a default format and one with an explicit format. We will cover formats in more detail in Section 21.3, Selecting a Data Representation, on page 457.

But first, let’s create a simple application to play with this. By now, you know the drill, so we’ll take it quickly. We’ll create an application called restful:

```
work> rails restful
```

So, now we’ll start creating our model, controller, views, and so on. We could do this manually, but Rails comes ready-made to produce scaffolding that uses resource-based routing, so let’s save ourselves some typing. The generator takes the name of the model (the resource) and optionally a list of field names and types. In our case, the article model has three attributes: a title, a summary, and the content:

```
restful> ruby script/generate scaffold article \
  title:string summary:text content:text
exists    app/models/
exists    app/controllers/
exists    app/helpers/
create    app/views/articles
exists    app/views/layouts/
exists    test/functional/
exists    test/unit/
exists    public/stylesheets/
```