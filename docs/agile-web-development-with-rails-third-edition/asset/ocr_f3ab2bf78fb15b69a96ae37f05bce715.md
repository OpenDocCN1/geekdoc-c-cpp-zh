The list displayed by this example will be identical to that of the first, but the values it communicates back to the application will be 1, or 2, or 3, or.... rather than Andy, Bert, or Chas. The HTML generated is as follows:

```
<select id="user_id" name="user[id]">
  <option value="1">Andy</option>
  <option value="2">Bert</option>
  <option value="3">Chas</option>
  <option value="4" selected="selected">Dave</option>
  <option value="5">Eric</option>
  <option value="6">Fred</option>
</select>
```

Finally, if you pass a hash as the choices parameter, the keys will be used as the display text and the values as the internal keys. Because it's a hash, you can't control the order of the entries in the generated list.

Applications commonly need to construct selection boxes based on information stored in a database table. One way of doing this is by having the model's find method populate the choices parameter. Although we show the find call adjacent to the select in this code fragment, in reality the find would probably be either in the controller or in a helper module.

```
<%= @users = User.find(:all, :order => "name").map { |u| [u.name, u.id] } form.select(:name, @users) %>
```

Note how we take the result set and convert it into an array of arrays, where each subarray contains the name and the id.

A higher-level way of achieving the same effect is to use collection_select. This takes a collection, where each member has attributes that return the display string and key for the options. In this example, the collection is a list of user model objects, and we build our select list using those models' id and name attributes.

```
<%= @users = User.find(:all, :order => "name") form.collection_select(:name, @users, :id, :name) %>
```

# Grouped Selection Lists

Groups are a rarely used but powerful feature of selection lists. You can use them to give headings to entries in the list. In Figure 23.2, on the next page, we can see a selection list with three groups.

The full selection list is represented as an array of groups. Each group is an object that has a name and a collection of suboptions. In the following