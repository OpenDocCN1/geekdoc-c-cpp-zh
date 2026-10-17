# # CHAPTER 10 Control Structures

```
```
"Each and All", "The Eternal Pan",
"Hamatreya", "Earth-Song", "Brahma");
#Henry D. Thoreau
$HDT = join("\n " , " Henry D. Thoreau ",
"Sympathy ", "Sic Vita",
"Friendship", "Prayer",
"Independence", "The Inward Morning",
"My Love Must Be as Free");
#Sarah Margaret Fuller
$SMF = join ("\n " , " Sarah Margaret Fuller ",
"Encouragement" , "Dryad Song",
"The Highlands", "Winged Sphinx",
"The Passion-Flower");
#Caroline Sturgis Tappan
$CST = join ("\n " , " Caroline Sturgis Tappan",
"Lyric" , "Life" ,
"Art and Artist" ,
"Lines" , "The Hero");
#3 Make a choice
if($Char eq 'a'){
	$ToPrint = $RWE;
}
elseif($Char eq 'b'){
	$ToPrint = $SMF;
}
elseif($Char eq 'c'){
	$ToPrint = $HDT;
}else{
	$ToPrint = $CST;
}
print "\n( . $Char . )". $ToPrint;
```
```