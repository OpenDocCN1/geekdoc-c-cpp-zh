# Putting It All Together

Code 9.6 shows the final code for ui-generatedcontent-properties.css created in this chapter. Notice that I've had to add individual cases for each chapter in the book so that they are all numbered correctly in the footer.

# Code 9.6 Final ui-generatedcontent-properties.css

```
/* *** ui-generatedcontent-properties.css ***/
* {
	quotes: 'u' 'v' 'x' 'y';
}
h1 {
	cursor: crosshair;
}
footer a {
	cursor: url('../images/chrome/cursor-02.png') 20 20, help;
}
footer a:prev:before {
	content: url('../images/chrome/bullet-02.png') ' Chapter ' counter(chapterNum) ' ';
}
footer a.next:before {
	content: 'Chapter ' counter(chapterNum) ' ';
	content-increment: chapterNum 2;
}
footer a.next:after {
	content: ' ' url('../images/chrome/bullet-01.png');
}
#chapter1 footer{
	counter-reset: chapterNum 0;
}
#chapter2 footer{
	counter-reset: chapterNum 1;
}
#chapter3 footer{
	counter-reset: chapterNum 2;
}
#chapter4 footer{
	counter-reset: chapterNum 3;
}
#chapter5 footer{
	counter-reset: chapterNum 4;
}
#chapter6 footer{
	counter-reset: chapterNum 5;
}
#chapter7 footer{
	counter-reset: chapterNum 6;
}
#chapter8 footer{
	counter-reset: chapterNum 7;
}
#chapter9 footer{
	counter-reset: chapterNum 8;
}
#chapter10 footer{
	counter-reset: chapterNum 9;
}
#chapter11 footer{
	counter-reset: chapterNum 10;
}
#chapter12 footer{
	counter-reset: chapterNum 11;
}
```