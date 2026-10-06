# 230 Plug-In JavaScript: 100 Solutions

You can also have a lot of fun changing the type to another value such as 'fade', 'zoom', or 'instant'; you may also want to experiment with modifying the w and h arguments to change the width and height (or both). Don't forget that you can also change multi to true or 1 and have a quite different type of menu, in the headings toggle their contents between being popped up and down.

# Using the 'hover' Action

If you plan to offer a hover effect, you'll need to lay out your HTML slightly differently so that objects you don't do so under the mouse and then cause an automatic (and unwanted) mouseover event to occur—which could result in popping up the wrong section.

Here's one way to modify the HTML to use the 'hover' action of the FoldingMenu() plug-in:

```
<span id='h1'>&lt;b&gt;News&lt;/b&gt;</span> |
<span id='h2'>&lt;b&gt;Sport&lt;/b&gt;</span> |
<span id='h3'>&lt;b&gt;Weather&lt;/b&gt;</span> |
<span id='h4'>&lt;b&gt;Links&lt;/b&gt;</span> |

<span id='c1'>
&nbsp;&raquo;&lt;a href='local.html'>Local News&lt;/a&gt;
&nbsp;&raquo;&lt;a href='world.html'>World News&lt;/a&gt;
&nbsp;&raquo;&lt;a href='entertainment.html'>Entertainment News&lt;/a&gt;
&nbsp;&raquo;&lt;a href='business.html'>Business News&lt;/a&gt;
&nbsp;&raquo;&lt;a href='technology.html'>Technology News&lt;/a&gt;
</span>

<span id='c2'>
&nbsp;&raquo;&lt;a href='football.html'>Football&lt;/a&gt;
&nbsp;&raquo;&lt;a href='baseball.html'>Baseball&lt;/a&gt;
&nbsp;&raquo;&lt;a href='hockey.html'>Hockey&lt;/a&gt;
&nbsp;&raquo;&lt;a href='soccer.html'>Soccer&lt;/a&gt;
</span>

<span id='c3'>
&nbsp;&raquo;&lt;a href='movies.html'>Movies&lt;/a&gt;
&nbsp;&raquo;&lt;a href='music.html'>Music&lt;/a&gt;
&nbsp;&raquo;&lt;a href='television.html'>Television&lt;/a&gt;
</span>

<span id='c4'>
&nbsp;&raquo;&lt;a href='home.html'>Home Page&lt;/a&gt;
&nbsp;&raquo;&lt;a href='articles.html'>Articles&lt;/a&gt;
&nbsp;&raquo;&lt;a href='videos.html'>Videos&lt;/a&gt;
&nbsp;&raquo;&lt;a href='podcasts.html'>Podcasts&lt;/a&gt;
</span>

<script>
window.onload = function () {
  headings = Array('h1', 'h2', 'h3', 'h4');
  contents = Array('c1', 'c2', 'c3', 'c4');

  FoldingMenu(headings, contents, 'click', 'inflate', 0,1,1,200,300);
}
</script>
```

![](bbox=[0.675, 0.946, 0.825, 0.958])