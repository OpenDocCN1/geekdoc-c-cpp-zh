There are two interesting things in this code. First, the form_for helper on line 1 sets up a standard HTML form. But it does more. The first parameter, :order, tells the method that it’s dealing with an object in an instance variable named @order. The helper uses this information when naming fields and when arranging for the field values to be passed back to the controller.

The :url parameter tells the helper what to do when the user hits the submit button. In this case, we’ll generate an HTTP POST request that’ll end up getting handled by the save_order action in the controller.

You’ll see that form_for sets up a Ruby block environment (this block ends on line 6). Within this block, you can put normal template stuff (such as the <p> tag). But you can also use the block’s parameter (form in this case) to reference a form context. We use this context on line 4 to add a text field to the form. Because the text field is constructed in the context of the form_for, it is automatically associated with the data in the @order object.

All these relationships can be confusing. It’s important to remember that Rails needs to know both the *names* and the *values* to use for the fields associated with a model. The combination of form_for and the various field-level helpers (such as text_field) give it this information. We can see this process in Figure 10.1, on the preceding page.

Now we can create the template for the form that captures a customer’s details for checkout. It’s invoked from the checkout action in the store controller, so the template will be called checkout.html.erb in the directory app/views/store.

Rails has form helpers for all the different HTML-level form elements. In the code that follows, we use text_field and text_area helpers to capture the customer’s name, e-mail, and address:

```
```erb
<div class="depot-form">

  <%#= error_messages_for 'order' %>

  <% form_for :order, :url => { :action => :save_order } do |form| %>
    <fieldset>
      <legend>Please Enter Your Details</legend>

      <div>
        <% form.label :name, "Name:" %>
        <% form.text_field :name, :size => 40 %>
      </div>

      <div>
        <% form.label :address, "Address:" %>
        <% form.text_area :address, :rows => 3, :cols => 40 %>
      </div>
```
```