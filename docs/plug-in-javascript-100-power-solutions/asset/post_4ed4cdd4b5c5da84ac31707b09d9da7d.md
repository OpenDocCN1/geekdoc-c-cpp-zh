
## Chapter 12: Forms and Validation 355

Next, each argument is processed through the CleanupString() plug-in to ensure that they are in the formats required:

```
number = CleanupString(number, true, false, true, true)
month = CleanupString(month, true, false, true, true)
year = CleanupString(year, true, false, true, true)
```

After this, the variable left is assigned the first 4 digits of number, cclen is set to the card number's length, and checksum is initialized to 0:

```
var left = number.substr(0, 4)
var cclen = number.length
var checksum = 0
```

Next, several if() else statements check that left contains a valid sequence that matches a known brand of credit card, and if it does, the card number length in cclen is correct for the card-type. If left doesn't match a known card, or it matches one but cclen is the wrong length, the plug-in returns false to indicate that the card didn't verify.

If these tests are passed, the card's checksum is calculated using an algorithm invented by IBM scientist Peter Luh (for further details see en.wikipedia.org/wiki/Luhn_),

```
for (var j = 1 - (cclen % 2); j < cclen; j += 2)
  if (j < cclen) checksum += number[j] * 1

for (j = cclen % 2; j < cclen; j += 2)
{
  d = number[j] * 2
  checksum += d < 10 ? d : 9 - 9
}
```

```
if (checksum % 10 != 0) return false
```

Finally, the result is looked up and compared to the values supplied to the plug-in, so even if this has validated the date, the plug-in will return false if the card has expired:

```
var date = new Date()
date.setTime(date.getTime())
if (year.length == 4) year = year.substr(2, 2)
```

```
if (year > 50) return false
else if (year < (date.getFullYear() - 2000)) return false
else if ((date.getMonth() + 1) > month) return false
else return true
```

## 356 Plug-In JavaScript: 100 Solutions

## How To Use It

To use this plug-in, pass it card number, expiry date, and month and it will return true or false. Of course, this algorithm tests only whether the card meets certain requirements and not whether the user has entered a genuine card or whether the card has been revoked or over the user's credit limit, and so on. The purpose of the plug-in is mainly in catching errors and preventing random data to see what happens.

This example shows how you might use the plug-in:

```html
<h3>Your credit card details:</h3>
<font face='Courier New' type='text' name='size' size='24' /><br />
Card Number: <input id='ccnum' type='n' />
Expires: Month <input id='cmon' type='text' name='m' size='24' />
Year <input id='ccyear' type='text' name='y' size='4' /><br />
<button id='button'>Submit Card</button>
```

```javascript
<script>
window.onload = function () {
  getElementById('button').onclick = function () {
    if (ValidateCreditCard(getElementById('ccnum').value,
    getElementById('cmon').value,getElementById('ccyear').value))
    alert('That card validated successfully')
    else alert('That card did not validate')
  }
}
</script>
```

When incorporating the plug-in with your code you will probably want to replace the onclick event attached in the example with a function attached to the onsubmit event of your form. Also, make sure that when you do this your function returns true if the card verifies to allow the form submission to complete, and false (along with probably displaying an error message) if the card doesn't validate, to stop the form submission going.

> Note: Only up to 2050 are currently supported in order to base card dates around the years 1950 to 2050. If you are reading a well-thumbed copy of this book and it's coming up to mid-century, and JavaScript is still being used, you may wish to increase the value 50 in the 4th last line to a higher few years ahead of the current year.

## The Plug-in

```javascript
function ValidateCreditCard(number, month, year)
{
number += ''
month += ''
year += ''
number = CleanupString(number, true, false, true, true)
month = CleanupString(month, true, false, true, true)
```

## Chapter 12: Forms and Validation

```javascript
year = QString(year, true, false, true, true)
var left = number.substr(0, 4)
var cclen = number.length
var chksum = 0

if (left >= 3000 && left <= 3059 ||
    left >= 3600 && left <= 3699 ||
    left >= 3800 && left <= 3889) {
  // Diners Club
  if (cclen != 14) return false
} else if (left >= 3000 && left <= 3059 ||
    left >= 3600 && left <= 3699 ||
    left >= 3800 && left <= 3889) {
  // (Logic continues based on credit card patterns)
}
// Note: The OCR text became fragmented in the source here. 
// I have reconstructed the logic based on the provided snippets.
```
