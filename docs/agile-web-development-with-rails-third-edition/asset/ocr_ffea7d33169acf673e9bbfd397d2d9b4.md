We're also constructing our query string by parsing out the draggable item's database id from its DOM id. Look at that JavaScript snippet:

```
"'todo=' + encodeURIComponent(element.id.split('_').last())"
```

The with parameter takes a snippet and feeds it the actual DOM element that was dropped as a variable called element. In our partial, we defined the ids of those elements as todo_database id, so when we want to send the server information on which item was dropped, we split the todo back off and send only the database id.

We've also defined a simple style for the drop targets and draggable elements:

```
<style>
.hover {
  background-color: #888888;
}
#pending_todos ul li, #completed_todos ul li {
  list-style: none;
  cursor: -moz-grab;
}
#pending_todos, #completed_todos {
  border: 1px solid gray;
}
</style>
```

The hover class causes the drop target to highlight when a draggable item is poised on top of it. The second rule specifies that any <li> elements within the pending_todos or competed_todos will use the -moz-grab cursor, the grasping hand icon, in order to provide a visual cue to the user that the item has a special property (draggability). The last rule just draws a border around our drop targets to make them obvious.

What if you wanted to create a sortable list instead of two or more categories of items? Sorting usually involves a single list whose order you want sent back to the server whenever it is changed. To create one, you need only to be able to create an HTML list and then specify what to do when the order changes. The helper takes care of the rest.

```
<ul id="priority_todos">
  <% for todo in @todos %>
  <li id="todo_<%= todo.id %>"><%= todo.name %></li>
  <% end %>
</ul>
<%= sortable_element 'priority_todos',
  :url => {:action => 'sort_todos'} %>
```

The sortable_element helper can take any of the standard Prototype options for controlling what happens before, during and after the XHR call to the server.