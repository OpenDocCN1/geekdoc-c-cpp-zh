# Mark required fields.

```
```html
<form id="registration">
<p>
<label for="user_first_name">First name</label>
<input type="text" name="user[first_name]" id="user_first_name" class="required text" />
</p>
<!-- ...more fields... -->
<p class="radios">
<input type="checkbox" id="terms" name="terms" class="required" />
<label for="terms">I accept the terms of service*</label>
</p>
<p><input type="submit" value="Sign me up! " /></p>
</form>
```
```

# Detect missing required fields.

```
```js
function checkForm(e) {
  var firstOffender, value;
  this.select('.required').each(function(field) {
    value = field.getValue();
    if (value && !value.blank()) {
      field.up('p').removeClassName('missing');
    } else {
      firstOffender = firstOffender || field;
      field.up('p').addClassName('missing');
    }
  });
  if (firstOffender) { e.stop(); firstOffender.focus(); }
}
document.observe('dom:loaded', function() {
  $('registration').observe('submit', checkForm);
});
```
```

# Related Tasks

• Task 22, Validating Forms: Going Further, on the next page

• Task 23, Validating Forms: The Whole Nine Yards, on page 68