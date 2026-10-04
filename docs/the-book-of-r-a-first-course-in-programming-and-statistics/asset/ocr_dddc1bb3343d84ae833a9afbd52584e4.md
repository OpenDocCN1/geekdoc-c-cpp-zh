# ### 1.4.1 Coding

As mentioned, when you code with R, you execute the code in the console, possibly after writing the script in the editor first. The following points are importantant to note:

+   * R code's entered directly into the console for execution is shown preceded by the R > prompt and followed by any output displayed in the console. For example, this simple division of 14 by 6 from Section 2.1.1 looks like this:

```
R> 14/6
[1] 2.333333
```

+   * For code that should be written in the editor before it's executed in the console, I'll indicate as such in the text, and the code will be presented without the prompt. The following example comes from Section 10.2.1:

```
for(myitem in 5:7){
cat("--BRACED AREA BEGINS--\n")
cat("the current item is-",myitem,"\n")
cat("--BRACED AREA ENDS--\n")
}
```

My preferred coding style for actually arranging and indenting chunks like will become clearer as you progress through Part II.

+   * There will occasionally be long lines of code (either executed directly in the console or written in the editor), which for the sake of print, will be split and indented at an appropriate place to fit on the page. For example, this line from Section 6.2.2:

```
R> ordfac.vec <- factor(x("Small","Large","Large","Regular","Small"), levels=c("Small","Regular","Large"), ordered=TRUE)
```
Although this can be written out as a single line using R, you can also break the line at a comma (in this case, the comma splits the arguments to the level of the opening parenthesis of the relevant function). The broken line will be indented to the opening parenthesis of. Both forms—single line or split—will work as when is executed in R.

+   * In a couple of places when the console output is lengthy and not essential to your understanding of the immediate content, it'll be suppressed for the sake of print. I'll say as much as in the text, and you'll see the designation --snip-- in the affected chunk of code.