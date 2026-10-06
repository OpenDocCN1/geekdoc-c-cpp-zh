# 264 Plug-In JavaScript: 100 Power Solutions

After that, the ctrl counter is tested against the value in len. If they match, the text has completed being typed; otherwise, there is more to be typed, so ctrl is incremented, like this:

```
if (ctrl++ == len)
{}
```

Inside the if (id) statement, ctrl is reset to 0 ready for the next repeat (if there is one) and ctrl2 is incremented within another if (id) statement and compared with the number argument. If they match, all repeats have finished and the TT_Flag property is set to false, the repeating interrupts are cancelled with a call to clearInterval(), and the final underline character (which was previously added to str) is stripped from it using a call to substr(), as follows:

```
ctrl = 0

if (++ctrl2 == number)
{}
```

```
O(id).TT_Flag = false
clearInterval(id)
str = str.substr(0, len)
```

Next, because browsers use different properties for the value, if the browser supports the innerText property, it is assigned to str; otherwise, the textContent property of id is assigned to value, like this:

```
if O(id).innerText) O(id).innerText = str
else O(id).textContent = str
```

Then the function returns, and if the interrupts have not been cleared, it will be called up in another freq milliseconds.

# How To Use It

To use this plug-in, put some text in a container, such as a div or span, and pass that container to the plug-in with the number of repeats and the length of time it should take to complete the typing.

Here's a simple example that types out a simple phrase once, over a period of five seconds:

```
<font face='Courier New' size='6'><b></b>
<div id='text'>The quick brown fox jumps over the lazy dog.</div>
</font>
```

```
<script>
window.onload = function() {
{
TextType('text', 1, 5000)
}
</script>
```