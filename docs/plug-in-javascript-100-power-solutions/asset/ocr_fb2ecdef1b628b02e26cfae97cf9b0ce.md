# 272 Plug-In JavaScript: 100 Power Solutions

```
TextToMatrix('text', 3000)
FadeOut('text', 3000)
</script>
```

Note that I sniff in a call to the FadeOut() plug-in in this example as it makes for an interesting combined effect of the scrambling text slowly fading away—this is just one example of how you can combine these plug-in to produce more complex and interesting results.

You may also notice that I omitted the interruptible argument to FadeOut(). Therefore, this passes a value of 'undefined' for argument to the function, which will be treated as if the value was false and so it saves on typing.

# The Plug-In

```
function TextToMatrix(id, msecs)
  if (id instanceof Array)
  {
    for (var j = 0 ; j < id.length ; ++j)
      TextToMatrix(id[j], msecs)
  }

if (O(id).TM_Flag) return
else O(id).TM_Flag = true

var text
  = Html(id)
var len
  = text.length
var freq
  = Math.round(msecs / INTERVAL)
var count
  = 0
var chars
  = 'ABCDEFGHIKLMNOPQRSTUVWXYZ' + \
    'abcdefghijklmnopqrstuvwxyz' + ' + \
    '0123456789'
var id
  = setInterval(TextToMatrix, freq)
function TextToMatrix(
{
  for (var j = 0 ; j < len / 20 ; ++j)
  {
    var k
      = Math.floor(Math.random() * len)
    var l
      = Math.floor(Math.random() * chars.length)
  }

  if (text[k] == '\n' && text[k] == 'r' && text[k] == ' ')
    text = text.substr(0, k) + chars[l] + text.substr(k + 1)

  if (O(id).innerText) O(id).innerText = text
  O(id).textContent = text
```