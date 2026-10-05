To create an object in our game, we define some properties with make-property, define a predicate with make-type, get the predicate's associated instantiator with type-instantiator, and call that instantiator with appropriate arguments.

How do we make a troll? The make-troll constructor for a troll takes arguments that specify the values for properties that are specific to the particular troll being constructed. The troll will be created in a given place with a restlessness (proclivity to move around), and an acquisitiveness (proclivity to take things), and a hunger (proclivity to bite other people).

```
(define (create-troll name place restlessness hunger)
  'name name
  'location place
  'restlessness restlessness
  'acquisitiveness 1/10
  'hunger))
```

We create two trolls: grendel and registrar. They are initially placed in random places, with some random proclities.

```
(define (create-trolls places)
  (map (lambda name)
    (create-troll name
      (random-choice places)
      (random-bias 3)
      (random-bias 3)))
'(grendel registrar)))
```

The procedure random-choice randomly selects one item from the list it is given. The procedure random-bias chooses a number (in this case 1, 2, or 3) and returns its reciprocal.

The troll is defined as a predicate that is true only of trolls. The make-type procedure is given a name for the type and a descriptor of the properties that are specific to trolls. (Only trolls have a hunger property).

```
(define troll:hunger)
  (make-property 'hunger predicate bias))
```

```
(define troll?)
  (make-type 'troll (list troll:hunger))
```