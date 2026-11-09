
And finally, we add the content, which will make it look like the code below. Now that we've added the table content, we can refresh the See Us Play page to view the result.

```html
<h2>Upcoming Concerts</h2>
<table>
<tr><th>Date</th><th>Place</th><th>Time</th><th>Price</th>
</tr>
<tr>
<td>Sunday, June 12</td><td>Theatre</td><td>7:30 pm</td><td>$5.00</td>
</tr>
<tr>
<td>Wednesday, June 15</td><td>College</td><td>8:00 pm</td><td>Free!</td>
</tr>
<tr>
<td>Saturday, July 10</td><td>Bandstand</td><td>11:00 am</td><td>Free!</td>
</tr>
<tr>
<td>Sunday, July 11</td><td>Bandstand</td><td>2:00 pm</td><td>Free!</td>
</tr>
<tr>
<td>Sunday, August 28</td><td>Theatre</td><td>7:30 pm</td><td>$5.00</td>
</tr>
</table>
```

It looks a little jumbled up at the moment - but some work with our stylesheet should soon fix that!

![](img/52e45ce976f775dd17fd84d91912f770_51_0.png)

## ‹A STYLISH TABLE!›

![](img/52e45ce976f775dd17fd84d91912f770_52_0.png)

To make our jumbled-up table look more attractive we'll return to our CSS stylesheet. Go through the steps below, adding one line at a time to the stylesheet and clicking the refresh button on your web browser after each new line has been added.

- 1.

```css
table {
  font-size:70%;

  th, td {
  }
  th {
  }
  td {
  }
}
```

Makes all the text inside the table smaller. The value is entered as a percentage of the font size on the rest of the page.

![](img/52e45ce976f775dd17fd84d91912f770_52_1.png)

- 2.

```css
table {
  font-size:70%;
  width:100%;

  th, td {
  }
  th {
  }
  td {
  }
}
```

Makes the table cover the full width of the body area.

![](img/52e45ce976f775dd17fd84d91912f770_52_2.png)

- 3.

```css
table {
  font-size:70%;
  width:100%;
  th, td {
    border:1px solid #000000;
  }
  th {
  }
  td {
  }
}
```

Adds a 1-pixel-wide, solid, black border to each **th** and **td** element in the table. Notice that each element has its own separate border. This is not the effect we're looking for, so we'll fix that next. The first part of the rule is **th, td** which, thanks to the comma between the element names, means “apply this rule to **th** and **td** elements”.

![](img/52e45ce976f775dd17fd84d91912f770_52_3.png)

- 4.

```css
table {
  font-size: 70%;
  border-collapse: collapse;
  width: 100%;
}
th, td {
  border: 1px solid #000000;
}
th {
}
td {
}
```

We return to the table rule and set the **border-collapse** property to **collapse**. This merges the borders of the individual cells, creating a nicer visual effect.

| Date | Place | Time | Price |
|---|---|---|---|
| Sunday, June 12 | Theatre | 7:30 pm | $5.00 |
| Wednesday, June 15 | College | 8:00 pm | Free! |
| Saturday, July 10 | Bandstand | 11:00 am | Free! |
| Sunday, July 11 | Bandstand | 2:00 pm | Free! |
| Sunday, August 28 | Theatre | 7:30 pm | $5.00 |

- 5.

```css
table {
  font-size: 70%;
  border-collapse: collapse;
  width: 100%;
}
th, td {
  border: 1px solid #000000;
  padding: 8px;
}
th {
}
td {
}
```

Now we add some padding around the text in the **th** and **td** elements. This makes the contents of the table easier to read.

| Date | Place | Time | Price |
|---|---|---|---|
| Sunday, June 12 | Theatre | 7:30 pm | $5.00 |
| Wednesday, June 15 | College | 8:00 pm | Free! |
| Saturday, July 10 | Bandstand | 11:00 am | Free! |
| Sunday, July 11 | Bandstand | 2:00 pm | Free! |
| Sunday, August 28 | Theatre | 7:30 pm | $5.00 |

- 6.

```css
table {
  font-size: 70%;
  border-collapse: collapse;
  width: 100%;
}
th, td {
  border: 1px solid #000000;
  padding: 8px;
  text-align: left;
}
th {
}
td {
}
```

The header text looks unbalanced centered, so we align it to the left.

| Date | Place | Time | Price |
|---|---|---|---|
| Sunday, June 12 | Theatre | 7:30 pm | $5.00 |
| Wednesday, June 15 | College | 8:00 pm | Free! |
| Saturday, July 10 | Bandstand | 11:00 am | Free! |
| Sunday, July 11 | Bandstand | 2:00 pm | Free! |
| Sunday, August 28 | Theatre | 7:30 pm | $5.00 |

- 7.

```css
table {
  font-size:70%;
  border-collapse: collapse;
  width: 100%;
}
th, td {
  border:1px solid #000000;
  padding:8px;
  text-align: left;
}
th {
  background-color: #FCAB68;
}
td {
}
```

We'd like to make the heading row stand out from the rest of the table, so we change its background color. We use a shade of orange that will complement the background color of the table. (#FCAB68 is the hexadecimal value for this shade).

| Date | Place | Time | Price |
|---|---|---|---|
| Sunday, June 12 | Theatre | 7:30 pm | $5.00 |
| Wednesday, June 15 | College | 8:00 pm | Free! |
| Saturday, July 10 | Bandstand | 11:00 am | Free! |
| Sunday, July 11 | Bandstand | 2:00 pm | Free! |
| Sunday, August 28 | Theatre | 7:30 pm | $5.00 |

- 8.

```css
table {
  font-size:70%;
  border-collapse: collapse;
  width: 100%;
}
th, td {
  border:1px solid #000000;
  padding:8px;
  text-align: left;
}
th {
  background-color: #FCAB68;
}
td {
  background-color: #BA99C0;
}
```

And finally we decide to use a dark shade of purple (#BA99C0) for the background to the main part of the table.

| Date | Place | Time | Price |
|---|---|---|---|
| Sunday, June 12 | Theatre | 7:30 pm | $5.00 |
| Wednesday, June 15 | College | 8:00 pm | Free! |
| Saturday, July 10 | Bandstand | 11:00 am | Free! |
| Sunday, July 11 | Bandstand | 2:00 pm | Free! |
| Sunday, August 28 | Theatre | 7:30 pm | $5.00 |

For a more detailed look at colors and how you can choose them, turn back to page 30.

## «HELPING YOU GET AROUND»

### STYLING THE MENU LINKS

The Nanonauts would like to make some changes to the top menu to make it easier for users of the site to find their way from one page to another. There are two things they'd like to do:

- When you land on, for example, the See Us Play page, the See Us Play menu item should appear in light gray rather than black and you shouldn't be able to click it, because it would take you to the page you're already on!

![](img/52e45ce976f775dd17fd84d91912f770_55_0.png)

- When you roll over the other menu items, the links should change to underlined to show that they are active.

![](img/52e45ce976f775dd17fd84d91912f770_55_1.png)

![](img/52e45ce976f775dd17fd84d91912f770_55_2.png)

To style your links like those above you'll need to edit both the HTML files and the CSS file.

- 1. In each of your HTML files remove the link from each menu that leads to the same page. For example, in the `about-us.html` page you will remove the `<a href="about-us.html">` link, in the `playing-a-concert.html` page you will remove the `<a href="playing-a-concert.html">` link, and so on.
- 2. Add a `class` attribute with a value of `selected` to the `li` elements from which you removed the link. The two changes are shown in the before and after tables below.

### Menu code before editing

### Menu code after editing

| Menu code before editing | Menu code after editing |
|---|---|
| ```html
<nav>
<ul>
<li><a href="index.html">Home</a></li>
<li><a href="about-us.html">About Us</a></li>
<li><a href="our-songs.html">Our Songs</a></li>
<li><a href="see-us-play.html">See Us Play</a></li>
<li><a href="playing-a-concert.html">Playing a Concert</a></li>
</ul>
</nav>
``` | ```html
<nav>
<ul>
<li><a href="index.html">Home</a></li>
<li class="selected">About Us</li>
<li><a href="our-songs.html">Our Songs</a></li>
<li><a href="see-us-play.html">See Us Play</a></li>
<li><a href="playing-a-concert.html">Playing a Concert</a></li>
</ul>
</nav>
``` |

### our-songs.html

```html
<nav>
  <ul>
    <li><a href="index.html">Home</a></li>
    <li><a href="about-us.html">About Us</a></li>
    <li><a href="our-songs.html">Our Songs</a></li>
    <li><a href="see-us-play.html">See Us Play</a></li>
    <li><a href="playing-a-concert.html">Playing a Concert</a></li>
  </ul>
</nav>
```

```html
<nav>
  <ul>
    <li><a href="index.html">Home</a></li>
    <li><a href="about-us.html">About Us</a></li>
    <li class="selected">Our Songs</li>
    <li><a href="see-us-play.html">See Us Play</a></li>
    <li><a href="playing-a-concert.html">Playing a Concert</a></li>
  </ul>
</nav>
```

### see-us-play.html

```html
<nav>
  <ul>
    <li><a href="index.html">Home</a></li>
    <li><a href="about-us.html">About Us</a></li>
    <li><a href="our-songs.html">Our Songs</a></li>
    <li><a href="see-us-play.html">See Us Play</a></li>
    <li><a href="playing-a-concert.html">Playing a Concert</a></li>
  </ul>
</nav>
```

```html
<nav>
  <ul>
    <li><a href="index.html">Home</a></li>
    <li><a href="about-us.html">About Us</a></li>
    <li><a href="our-songs.html">Our Songs</a></li>
    <li class="selected">See Us Play</li>
    <li><a href="playing-a-concert.html">Playing a Concert</a></li>
  </ul>
</nav>
```

### playing-a-concert.html

```html
<nav>
  <ul>
    <li><a href="index.html">Home</a></li>
    <li><a href="about-us.html">About Us</a></li>
    <li><a href="our-songs.html">Our Songs</a></li>
    <li><a href="see-us-play.html">See Us Play</a></li>
    <li><a href="playing-a-concert.html">Playing a Concert</a></li>
  </ul>
</nav>
```

```html
<nav>
  <ul>
    <li><a href="index.html">Home</a></li>
    <li><a href="about-us.html">About Us</a></li>
    <li><a href="our-songs.html">Our Songs</a></li>
    <li><a href="see-us-play.html">See Us Play</a></li>
    <li class="selected">Playing a Concert</li>
  </ul>
</nav>
```
