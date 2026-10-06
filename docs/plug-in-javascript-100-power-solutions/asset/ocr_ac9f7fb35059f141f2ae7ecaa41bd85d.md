# 326 Plug-In JavaScript: 100 Power Solutions

# The Plug-in

```
function ProcessCookie(action, name, value, seconds, path,
domain, secure)
{
  if (action == 'save') {
    var date = new Date();
    date.setTime(date.getTime() + seconds * 1000);
    var expires = seconds ? '; expires=' + date.toUTCString() : '';
    path = path ? '; path=' + path : '';
    domain = domain ? '; domain=' + domain : '';
    secure = secure ? '; secure=' + secure : '';
    document.cookie = name + '=' + escape(value) + expires + path;
  } else if (action == 'read') {
    if (!document.cookie.length) return false;
    else {
      var start = document.cookie.indexOf(name + '=');
      if (start == -1)n      {
        start += name.length + 1;
        var end = document.cookie.indexOf(';', start);
        end = (end == -1) ? document.cookie.length : end;
        return unescape(document.cookie.substring(start, end));
      }
    }
  } else if (action == 'erase')
    ProcessCookie('save', '', -60)
}
```

# 85 CreateAjaxObject()

Ajax is the power behind the vastly improved user interaction of Web 2.0. It stands for Asynchronous JavaScript and XML, which is really a contrived acronym for a background call to a web server. Using this plug-in, you can easily create a new Ajax object that can be used to send and request information to and from a web server in the background, without the user being aware of it.

Unlike the past, when a POST or GET stopped action in the browser until it completed, with Ajax the browser handles the request without disrupting the web application.

Figure 11-2 shows a simple HTML file that has been fetched from the web server and inserted into a div, using this plug-in in connection with the next one, GetAjaxRequest().

![](bbox=[0.035, 0.693, 0.115, 0.725])