# Plug-In JavaScript: 100 Solutions

Next, each character in html that will have its font size processed within a for() loop that the outside characters of the group are the smallest, the one just in from them are larger, and the largest one is in the center, as follows:

```
for (var j = 0; j < 7; j++)
  temp += InsVars('font size='+#'#2/font',
                4 - Math.abs(j - 3), html.substr(ctrl, j));
```

The part determines that this gives font size values (Math.abs(j - 3)), which for the values 0 through 6 of j, gives the following font size makes all negative numbers: 1, 2, 3, 4, 3, 2, 1.

Once all font sizes have been calculated and stored in temp using the InsVars() plug-in to insert the values into a string containing <font size...> statements, the innerHTML.property of id is assigned to this string to display it, along with the remaining, unchanged portion of html:

```
Html(id, temp + html.substr(ctrl + j))
```

An if() statement increments ctrl and checks whether it equals the value in len. If so, the animation has finished and the following code is executed:

```
if (++ctrl == len)
{
```

If the ripple is finished, ctrl is reset and if() statement checks whether there are more repeats of the interrupting ripple, like:

```
ctrl = 0
if (ctrl2 == number)
{
  if (O(id).innerText) O(id).innerText = html
  else O(id).textContent = html

  O(id).TR_Flag = false
  clearInterval(iid)
}
```

If the repeats have finished, the value in html is saved back into as text, not HTML (Otherwise, unwanted extra HTML tags would be added by the browser--the time for saving HTML to the property is only when the font sizes are being changed).
Next, the TR_Flag property of id is set to false to indicate that all ripples have completed, and the clearInterval(iid) function is called to stop any future calls to the subfunction, passing the value previously stored iid.

The function then returns but will be called again in freq milliseconds if there are still animation frames to draw.

# How To Use It

To use this animation, pass an object, such as a div or span containing only text with HTML markup or other tags; tell it the number of times to repeat the ripple; and give it the length of time in milliseconds that the animation should take.