The user mouses over the name field, getting an indication that the field is editable:

Username: anders gosling
Favorite language: [Click to edit]
Edit | Back

And here’s what the page looks like in full edit mode for the name field:

Username: anders gosling ok cancel
Favorite language: Rails
Edit | Back

If you stick with the default settings, this is incredibly easy to create. In your controller, specify the name of the model class and column names you want your controller to support in-place editing for:

```
class UserController < ApplicationController
  in_place_edit_for :user, :username
  in_place_edit_for :user, :favorite_language
  # ...
```

These helper methods actually create methods called set_user_username and set_user_favorite_language in your controller that the form will interact with to update the field data. These generated methods will update the current model instance with the new data and return the newly saved value.

Use the in_place_editor_field helper to create the control. In our example, we just iterate over all the columns on the model and create one for each:

Download pragforms/app/views/user/inplace_demo.html.erb

```
<% for column in User.user_columns %>
<p>
  <b><%= column.human_name %>:</b>
  <%= in_place_editor_field "user", column.name, {}, {
    :load_text_url=> url_for(:action=>"get_user_#{column.name}", :id=>@user)
  } %>
</p>
<% end %>

<%= link_to 'Edit', :action => 'edit', :id => @user %> |
<%= link_to 'Back', :action => 'list' %>
```

That’s all you need to create the default version. You can specify plenty of options to alter the default behavior, however.