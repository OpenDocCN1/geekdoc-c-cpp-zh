# Selection Lists

Selection lists are those drop-down list boxes with the built-in artificial intelligence that guarantees the choice you want can be reached only by scrolling past everyone else’s choice.

Selection lists contain a set of choices. Each choice has a display string and an optional value attribute. The display string is what the user sees, and the value attribute is what is sent back to the application if that choice is selected. For regular selection lists, one choice may be marked as being selected; its display string will be the default shown to the user. For multiselect lists, more than one choice may be selected, in which case all of their values will be sent to the application. A basic selection list is created using the select helper method:

```
form.select(:attribute, choices, options, html_options)
```

The choices parameter populates the selection list. The parameter can be any enumerable object (so arrays, hashes, and the results of database queries are all acceptable).

The simplest form of choices is an array of strings. Each string becomes a choice in the drop-down list, and if one of them matches the current value of @variable.attribute, it will be selected. (These examples assume that @user.name is set to Dave.)

Download e1/views/app/views/test/select.html.erb

```
<% form_for :user do |form| %>
  <%= form.select(:name, %{ Andy Bert Chas Dave Eric Fred }) %>
<% end %>
```

This generates the following HTML:

```
<select id="user_name" name="user[name]">
  <option value="Andy">Andy</option>
  <option value="Bert">Bert</option>
  <option value="Chas">Chas</option>
  <option value="Dave" selected="selected">Dave</option>
  <option value="Eric">Eric</option>
  <option value="Fred">Fred</option>
</select>
```

If the elements in the choices argument each respond to first and last (which will be the case if each element is itself an array), the selection will use the first value as the display text and the last value as the internal key:

Download e1/views/app/views/test/select.html.erb

```
<%= form.select(:id, [ ['Andy', 1],
  ['Bert', 2],
  ['Chas', 3],
  ['Dave', 4],
  ['Eric', 5],
  ['Fred', 6]]) %>
```