# Mark up the login field.

Download form/validation_ajax/index.html

```
<p>
  <label for="user_login">Login</label>
  <input type="text" name="user[login]" id="user_login" class="required text" />
  <span class="feedback" style="display: none;"></span>
  <img src="spinner.gif" class="spinner" style="display: none;" />
</p>
```

# Watch the login.

Download form/validation_ajax/validation_ajax.js

```
document.observe('dom:loaded', function checkLogin() {
  var feedback = $('user_login').next('.feedback'),
      spinner = $('user_login').next('.spinner');
  new Field.Observer('user_login', 0.8, function(_, value) {
    if (value.length < 2) return;
    feedback.hide(); spinner.show();
    new Ajax.Request('check_login.php', {
      method: 'get', parameters: { login: value },
      onComplete: function(res) {
        if (Ajax.activeRequestCount > 1) return;
        if (res.request.success && res.status) {
          feedback.update('Login available!').removeClassName('ko');
        } else {
          feedback.update('Login taken!').addClassName('ko');
        }
        spinner.hide(); feedback.show();
      }
    });
  });
});
```

# Simulate the login.

Download form/validation_ajax/check_login.php

```
<?php
sleep(rand(5, 10) / 10.0); // Simulate intarwebs delay...
$RESERVED = array('bob', 'doudou', 'tdd', 'meshak', 'ook');
$login = isset($_GET['login']) ? $_GET['login'] : '';
$response = in_array($login, $RESERVED) ? '422 Conflict' : '202 Accepted';
header('HTTP/1.1 ' . $response);
?>
```