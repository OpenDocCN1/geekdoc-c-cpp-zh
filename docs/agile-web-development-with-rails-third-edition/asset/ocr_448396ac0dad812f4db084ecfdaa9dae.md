How do we get Rails to use our shiny new form builder? We simply add a :builder parameter to form_for:

```
Download e1/views/app/views/builder/new.html.erb
<% form_for :product, :url => { :action => :save },
  :builder => TaggedBuilder do |form| %>
  <%= form.text_field 'title' %>
  <%= form.text_area 'description' %>
  <%= form.text_field 'image_url' %>
  <%= submit_tag %>
<% end %>
```

If we're planning to use our new builder in multiple forms, we might want to define a helper method that does the same as form_for but that adds the builder parameter automatically. Because it's a regular helper, we can put it in helpers/application_helper.rb (if we want to make it global) or in a specific controller's helper file.

Ideally, the helper would look like this:

```
# DOES NOT WORK
def tagged_form_for(name, options, &block)
  options = options.merge(:builder => TaggedBuilder)
  form_for(name, options, &block)
end
```

However, form_for has a variable-length parameter list—it takes an optional second argument containing the model object. We need to account for this, making our final helper somewhat more complex:

```
Download e1/views/app/helpers/builder_helper.rb
module BuilderHelper
  def tagged_form_for(name, *args, &block)
    options = args.last.is_a?(Hash) ? args.pop : {}
    options = options.merge(:builder => TaggedBuilder)
    args = (args << options)
    form_for(name, *args, &block)
  end
end
```

Our final view file is now pretty elegant:

```
Download e1/views/app/views/builder/new_with_helper.html.erb
<% tagged_form_for :product, :url => { :action => :save } do |form| %>
  <%= form.text_field 'title' %>
  <%= form.text_area 'description' %>
  <%= form.text_field 'image_url' %>
  <%= submit_tag %>
<% end %>
```

Form builders are one of the unsung heroes of Rails. You can use them to establish a consistent and DRY look and feel across your application, and you