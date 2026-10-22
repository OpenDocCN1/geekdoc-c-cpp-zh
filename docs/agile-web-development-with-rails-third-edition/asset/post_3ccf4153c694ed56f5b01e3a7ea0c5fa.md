
```ruby
respond_to do |format|
  if @article.save
    flash[:notice] = 'Article was successfully created.'
    format.html { redirect_to(@article) }
    format.xml { render :xml => @article, :status => :created,
                  :location => @article }
  else
    format.html { render :action => "new" }
    format.xml { render :xml => @article.errors,
                  :status => :unprocessable_entity }
  end
end
end

# PUT /articles/1
# PUT /articles/1.xml
def update
  @article = Article.find(params[:id])

  respond_to do |format|
    if @article.update_attributes(params[:article])
      flash[:notice] = 'Article was successfully updated.'
      format.html { redirect_to(@article) }
      format.xml { head :ok }
    else
      format.html { render :action => "edit" }
      format.xml { render :xml => @article.errors,
                    :status => :unprocessable_entity }
    end
  end
end

# DELETE /articles/1
# DELETE /articles/1.xml
def destroy
  @article = Article.find(params[:id])
  @article.destroy

  respond_to do |format|
    format.html { redirect_to(articles_url) }
    format.xml { head :ok }
  end
end
```

Notice how we have one action for each of the RESTful actions. The comment before each shows the format of the URL that invokes it.

Notice also that many of the actions contain a respond_to block. As we saw back on page 185, Rails uses this to determine the type of content to send in a response. The scaffold generator automatically creates code that will respond appropriately to requests for HTML or XML content. We'll play with that in a little while.

The views created by the generator are fairly straightforward. The only tricky thing is the need to use the correct HTTP method to send requests to the server. For example, the view for the index action looks like this:

```erb
Download restful/app/views/articles/index.html.erb
<h1>Listing articles</h1>
<table>
  <tr>
    <th>Title</th>
    <th>Summary</th>
    <th>Content</th>
  </tr>

<% for article in @articles %>
  <tr>
    <td><%=h article.title %></td>
    <td><%=h article.summary %></td>
    <td><%=h article.content %></td>
    <td><%= link_to 'Show', article %></td>
    <td><%= link_to 'Edit', edit_article_path(article) %></td>
    <td><%= link_to 'Destroy', article, :confirm => 'Are you sure?', :method => :delete %></td>
  </tr>
<% end %>
</table>

<br />

<%= link_to 'New article', new_article_path %>
```

The links to the actions that edit an article and add a new article should both use regular GET methods, so a standard link_to works fine.⁶ However, the request to destroy an article must issue an HTTP DELETE, so the call includes the :method => :delete option to link_to.⁷

6. Note how we’re using named routes as the parameters to these calls. Once you go RESTful, named routes are de rigueur.

7. And here the implementation gets messy. Browsers cannot issue HTTP DELETE requests, so Rails fakes it out. If you look at the generated HTML, you’ll see that Rails uses JavaScript to generate a dynamic form. The form will post to the action you specify. But it also contains an extra hidden field named _method whose value is delete. When a Rails application receives a _method parameter, it ignores the real HTTP method and pretends the parameter’s value (delete in this case) was used.

For completeness, here are the other views:

```erb
Download restful/app/views/articles/edit.html.erb
<h1>Editing article</h1>

<% form_for(@article) do |f| %>
  <%= f.error_messages %>
```

```erb
<p>
  <b>Content:</b>
  <%= @article.content %>
</p>

<%= link_to 'Edit', edit_article_path(@article) %> |
<%= link_to 'Back', articles_path %>
```

## Adding Your Own Actions

In an ideal world you’d use a consistent set of actions across all your application’s resources, but this isn’t always practical. You sometimes need to add special processing to a resource. For example, we may need to create an interface to allow people to fetch just recent articles. To do that with Rails, we use an extension to the map.resources call:

```ruby
ActionController::Routing::Routes.draw do |map|
  map.resources :articles, :collection => { :recent => :get }
end
```

That syntax takes a bit of getting used to. It says “we want to add a new action named recent, invoked via an HTTP GET. It applies to the collection of resources—in this case all the articles.”

| Method | URL Path | Action | Helper |
|--------|----------|--------|--------|
| GET | /articles/recent | recent | recent_articles_url |

In fact, we’ve already seen this technique of appending special actions to a URL using a slash—the edit action uses the same mechanism.

You can also create special actions for individual resources; just use :member instead of :collection. For example, we could create actions that mark an article as embargoed or released—an embargoed article is invisible until released:

```ruby
ActionController::Routing::Routes.draw do |map|
  map.resources :articles, :member => { :embargo => :put,
    :release => :put }
end
```

This adds the following routes to the standard set added by map.resources:

| Method | URL Path | Action | Helper |
|--------|----------|--------|--------|
| PUT | /articles/1/embargo | embargo | embargo_article_url(:id => 1) |
| PUT | /articles/1/release | release | release_article_url(:id => 1) |

It’s also possible to create special actions that create new resources; use :new, passing it the same hash of :action => :method we used with :collection and :member. For example, we might need to create articles with just a title and a body—the summary is omitted.

We could create a special shortform action for this:

```ruby
ActionController::Routing::Routes.draw do |map|
  map.resources :articles, :new => { :shortform => :post }
end
```

This adds the following routes to the standard set added by map.resources:

| Method | URL Path | Action | Helper |
|--------|----------|--------|--------|
| POST | /articles/new/shortform | shortform | shortform_new_article_url |

## Nested Resources

Often our resources themselves contain additional collections of resources. For example, we may want to allow folks to comment on our articles. In this case, each comment would be a resource, and collections of comments would be associated with each article resource.

Rails provides a convenient and intuitive way of declaring the routes for this type of situation:

```ruby
ActionController::Routing::Routes.draw do |map|
  map.resources :articles do |article|
    article.resources :comments
  end

  # ...

  map.connect ':controller/:action/:id'
  map.connect ':controller/:action/:id.:format'
end
```

There even is a shorthand for the simplest and most common case, such as this one:

```ruby
map.resources :articles, :has_many => :comments
```

Both expressions are equivalent and define the top-level set of article routes and additionally create a set of subroutes for comments. Because the comment resources appear inside the articles block, a comment resource must be qualified by an article resource. This means that the path to a comment must always be prefixed by the path to a particular article. To fetch the comment with id 4 for the article with an id of 99, you'd use a path of /articles/99/comments/4.

Once again, we can see the full set of routes generated by our configuration by using the rake routes command:

```text
articles GET    /articles
            {:controller=>"articles", :action=>"index"}
formatted_articles GET    /articles.:format
            {:controller=>"articles", :action=>"index"}
POST   /articles
  {:controller=>"articles", :action=>"create"}
POST   /articles.:format
  {:controller=>"articles", :action=>"create"}
new_article GET    /articles/new
  {:controller=>"articles", :action=>"new"}
formatted_new_article GET    /articles/new.:format
  {:controller=>"articles", :action=>"new"}
edit_article GET    /articles/:id/edit
  {:controller=>"articles", :action=>"edit"}
formatted_edit_article GET    /articles/:id/edit.:format
  {:controller=>"articles", :action=>"edit"}
article GET    /articles/:id
  {:controller=>"articles", :action=>"show"}
formatted_article GET    /articles/:id.:format
  {:controller=>"articles", :action=>"show"}
PUT    /articles/:id
  {:controller=>"articles", :action=>"update"}
PUT    /articles/:id.:format
  {:controller=>"articles", :action=>"update"}
DELETE /articles/:id
  {:controller=>"articles", :action=>"destroy"}
DELETE /articles/:id.:format
  {:controller=>"articles", :action=>"destroy"}
article_comments GET    /articles/:article_id/comments
  {:controller=>"comments", :action=>"index"}
formatted_article_comments GET    /articles/:article_id/comments.:format
  {:controller=>"comments", :action=>"index"}
POST   /articles/:article_id/comments
  {:controller=>"comments", :action=>"create"}
POST   /articles/:article_id/comments.:format
  {:controller=>"comments", :action=>"create"}
new_article_comment GET    /articles/:article_id/comments/new
  {:controller=>"comments", :action=>"new"}
formatted_new_article_comment GET    /articles/:article_id/comments/new.:format
  {:controller=>"comments", :action=>"new"}
edit_article_comment GET    /articles/:article_id/comments/:id/edit
  {:controller=>"comments", :action=>"edit"}
formatted_edit_article_comment GET    /articles/:article_id/comments/:id/edit.:format
  {:controller=>"comments", :action=>"edit"}
article_comment GET    /articles/:article_id/comments/:id
  {:controller=>"comments", :action=>"show"}
formatted_article_comment GET    /articles/:article_id/comments/:id.:format
  {:controller=>"comments", :action=>"show"}
PUT    /articles/:article_id/comments/:id
  {:controller=>"comments", :action=>"update"}
PUT    /articles/:article_id/comments/:id.:format
  {:controller=>"comments", :action=>"update"}
DELETE /articles/:article_id/comments/:id
  {:controller=>"comments", :action=>"destroy"}
DELETE /articles/:article_id/comments/:id.:format
  {:controller=>"comments", :action=>"destroy"}
  /:controller/:action/:id
  /:controller/:action/:id.:format
```
