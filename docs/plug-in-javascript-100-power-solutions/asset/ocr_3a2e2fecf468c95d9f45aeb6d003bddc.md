# Chapter 9: Text Effects 269

# How To Use It

To use this plug-in, pass it an object, such as a div or span that contains some text, and tell it how long the reveal transition should take, as with this example:

```
<font face='Courier New' size='6'>
<div id='text'>Welcome to the best science fiction and fantasy fan
website in the world!</div>
</b></font>

<script>
window.onload = function() {
{
  MatrixToText('text', 3000)
}
</script>
```

# The Plug-in

```
function MatrixToText(id, msecs)
{
  if (id instanceof Array) {
    for (var j = 0; j < id.length; ++j)
      MatrixToText(id[j], msecs)
    return
  }

  if (O(id).MT_Flag) return
  else O(O(id).MT_Flag = true

  var html = Html(id)
  var len = html.length
  var freq = Math.round(msecs / INTERVAL)
  var matrix = ''
  var chars = 'ABCDEFGHIJKMNOPQRSTUVWXYZ' + +
    'abcdefghijklmnopqrstuvwxyz' + +
    '0123456789'

  for (var j = 0; j < len; ++j) {
    if (html[j] == '\n' || html[j] == ' ' ) matrix += html[j]
    else matrix += chars[Math.floor(Math.random()) * chars.length]
  }

  if (O(id).innerText) O(id).innerText = matrix
  else O(id).textContent = matrix
}

var iid = setInterval(DoMatrixToText, freq)

function DoMatrixToText()
```