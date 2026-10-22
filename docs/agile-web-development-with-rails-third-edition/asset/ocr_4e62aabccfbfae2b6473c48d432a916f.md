![](bbox=[0.38, 0.07, 0.62, 0.22])

# Figure 24.3: Choosing the first item

Autocomplete is just another server-side callback. As we've learned already, it is important to notify your users when these asynchronous calls are being made on their behalf. You can use the :indicator option to specify the DOM id of a graphic to toggle on at the start of the call and toggle off upon completion:

```
<%= text_field :user, :language %>
<img id='language_spinner' src='spinner.gif' style='display:none;' />
<div class="auto_complete" id="user_language_auto_complete"></div>
<%= auto_complete_field :user_language,
    :indicator => 'language_spinner' %>
```

If the user needs to enter more than one value per autocompleting text field, you can specify one or more tokens that can be used to reset the behavior as they type. For example, we could allow the user to choose multiple favorite languages for the programmer by using a comma to separate the values:

```
<%= text_field :user, :languages %>
<div class="auto_complete" id="user_languages_auto_complete"></div>
<%= auto_complete_field :user_languages,
    :tokens => ',' %>
```

As the user starts to enter a value, they'll get the list of choices, as shown in Figure 24.3. Then, if they make a selection and type in one of the tokens (in this case, a comma), the list will show again, and they can pick a second item, as shown in Figure 24.4, on the next page.

Finally, you can specify a JavaScript expression to be called when the target <div> is either shown or hidden (:on_show, :on_hide) or after the text field has been updated by the user's selection (:after_update_element). These callbacks allow you to specify other visual effects or even server-side actions in response to the user's interaction with the autocomplete field.

On the server, you will want to write an action that can turn a partial value into a list of potential matches and return them as an HTML snippet containing