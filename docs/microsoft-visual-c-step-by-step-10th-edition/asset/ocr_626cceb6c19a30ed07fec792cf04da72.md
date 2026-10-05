```
Horse myHorse = new Horse(...);
Mammal myMammal = myHorse; // myMammal refers to a Horse
...
Horse myHorseAgain = myMammal as Horse; // OK - myMammal was a Horse
...
Whale myWhale = new Whale(...);
myMammal = myWhale;
...
myHorseAgain = myMammal as Horse; // returns null - myMammal was a Whale
```