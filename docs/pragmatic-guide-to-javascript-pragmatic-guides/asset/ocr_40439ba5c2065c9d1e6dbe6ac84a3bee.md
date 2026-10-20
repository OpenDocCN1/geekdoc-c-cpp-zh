# Deciding what path to take

```
if (condition) {
  code
}

if (condA) {
  codeA
} else if (condB) {
  codeB
} else {
  codeC
}
```

```
switch (expr) {
  case valueA:
    codeA
    break;
  case valB1:
  case valB2:
    codeB
    break;
  default:
    codeC
}
```

Protip: early tests with returning code let you avoid nesting the rest in an else block and keep your indentation sane!

# Looping around

```
for (decl; test; incr) {
  code
}

do {
  codeRunAtLeastOnce
} while (cond)
```

```
while (cond) {
  codePerhapsNeverRun
}

while (true) {
  codeRunAtLeastOnce
  if (!skipRestOfTurn)
    continue;
  if (justStopLooping)
    break;
  remainderCode
}
```

"Fast array loop":

```
for (var i = 0, l = arr.length; i < l; ++i)
  code
```

# Array stuff you should know

```
var arr = [2, 3, 4, 5, 6];

arr.length                 // => 5
arr.concat([7, 8, 9])      // => [2,7,9]
arr                        // => [2,9]
arr.push(10)               // => [2,10]
arr.unshift(1)             // => [1,10]
arr.pop()                  // => 10
arr.shift()                // =>
arr.slice(4, -2)           // => [6, 7, 8]
arr.join('')               // => '23456789'

arr.sort(function(a, b) {
  return b - a;
}) // => [9, 8, 7, 6, 5, 4, 3, 2]
arr.sort()                 // => [2, 3, 4, 5, 6, 7, 8, 9]
arr.splice(5)              // => [7, 8, 9]
arr                        // => [2, 3, 4, 5, 6]
```

# Really useful String stuff

First, there's a length property (characters, not bytes).

```
'yay'.charAt(1)                // => 'a'
'hello'.indexOf('l')            // => 2
'hello'.indexOf('l', 3)         // => 3 (specified min pos)
'hello'.lastIndexOf('l')        // => 3
'hello'.lastIndexOf('l', 2)     // => 2 (specified max pos)
'hello'.replace(/l/, 'L')       // => 'heLlo'
'hello'.replace(/[aeiou]/g, '-') // => 'h-ll-'

'hello'.replace(/C(/I/g, function(s) {
  return s.toUpperCase();
}) // => 'HELLO'

'a b c'.split(' ')              // => ['a','b','c']
'a b c'.split(/\s+/)           // => ['a','b','c']
'abc'.split('')                 // => ['a','b','c']
'a b c'.split(' ', 2)           // => ['a','bc'] (specific max count)
'hello'.substring(2)            // => 'llo'
'hello'.substring(2, 4)         // => 'll' (specified end boundary)
'hello'.slice(-3)               // => 'llo' (start 3 from end)
'hello'.slice(3, -1)            // => 'll' (specified end boundary, 2 from end)
'Elodie'.toLowerCase()          // => 'elodie'
'déjà ça'.toUpperCase()         // => 'DÉJÀ ÇA'
'hello'.match(/C(/I)            // => ['l','l']
† full match at index 0, captured group 1 at index 1, etc.
```

# Exception/error handling

```
try {
  thisCodeMayExplode
} catch(e) {
  thisCodeRunsOnlyOnErrors // e refers to the error object
} finally {
  thisCodeRunsWhetherOrNotThereIsAnError
}
```

You can raise your own errors (any object will do) with raise exceptionObject

# Math functions

# A few global goodies

# Asynchronous code: using timeouts

# Poor man's debugger

# Identifiers and reserved words