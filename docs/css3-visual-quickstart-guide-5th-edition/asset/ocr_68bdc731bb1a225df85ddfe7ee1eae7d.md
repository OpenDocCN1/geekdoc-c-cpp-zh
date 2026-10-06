# Styling for interaction

Once loaded, Web pages are far from static. Users will start interacting with their pointers the right away, moving their pointers across the screen and clicking hither and yon. The dynamic pseudo-classes allow you to style elements as the user interacts with them, providing visual feedback:

Code 4.7 The input elements are set to change style when the user interacts with them by hovering, selecting (focussed), or clicking (active) 

+   * :hover—Same as for links, but sets the appearance of the element when the pointer is hovering over.

+   * :focus—Applied to elements that can receive focus, such as text fields.

+   * :active—Same as for links, but sets the style of the element when it is clicked or selected.

```
<!-- HTML -->
<DOCTYPE html>
<html lang="en">
<head>
  <meta http-equiv="Content-Type"
    content="text/html;charset=UTF-8" />
  <title>Alice's Adventures in Wonderland</title>
  <style type="text/css" media="all">
    input {
      border: 3px solid rgb(153,153,153);
      background-color: rgb(204,204,204);
      color: rgb(153,153,153);
      padding: 0px;
      font-size: 2em;
    }
    input:hover {
    border-color: rgb(204,153,153);
    color: rgb(102,102,102);
  }
  input:focus {
    border-color: rgb(255,0,0);
    background-color: rgb(255,255,255);
    color: rgb(0,0,0);
    outline: none;
  }
  input:active {
    border-color: rgb(255,0,0);
    background-color: rgb(0,0,0);
  }
</style>
</head>
<body>
  <input type="text" value="First Name">
  <input type="text" class="hover" value="Last Name">
  <input type="text" class="focus"
    value="Email"
  <input type="button" class="active"
    value="Search"
</form>
</body>
</html>
```

# To define a dynamic pseudo-class:

+   1. Style the default element.
input {...}

Although optional, it's generally a good idea to set the default, non-dynamic style for the elements receiving dynamic styles (Code 4.7).

+   2. Style the hover state of the element.
Type the selector (HTML, class, or ID), a colon (:), and then hover.
input:hover {...}

As the pointer enters the element's box (see Chapter 10 for details about the box model), the style change will occur.