
```scheme
(define (take-thing name)
  (let ((thing (find-thing name (here))))
    (if thing
        (take-thing! thing my-avatar)
        'done))
```

```scheme
(define (take-thing! thing person)
  (move! thing (get-bag person) person))
```

There are two procedures here. The first is a user-interface
procedure to give the player a convenient way of describing the thing
to be taken by giving its name. It calls the second, an internal
procedure that is also used in other places.

To make this work we supply a handler for generic-move! that
is specialized to moving mobile things from places:

```scheme
(define-generic-procedure-handler generic-move!
  (match-args mobile-thing? place? bag? person?)
  (lambda (mobile-thing from to actor)
    (let ((new-holder (get-holder to)))
      (cond (eqv? actor new-holder)
            (narrate! list actor
                  "picks up" mobile-thing
                  actor)
            else
            (narrate! list actor
                  "picks up" mobile-thing
                  "and gives it to" new-holder)
            actor))
      (if (not eqv? actor new-holder)
        (say! new-holder (list "Whoa!, dude!"))
      (move-internal! mobile-thing from to))))
```

The actor is taking the thing, the actor is the new-holder.

But it is possible that the actor is picking up the thing in the
place and putting it into someone's bag!

The say! procedure is used to indicate that a person has said
something. Its first argument is the person speaking, and the second
argument is the text being spoken. The move-internal
procedure actually moves the object from one place to another.

To drop a thing we use the procedure drop-thing to move it
from our bag to our current location:

```scheme
(define drop-thing name)
  (let ((thing (find-thing name my-avatar)))
    (if thing
        (drop-thing! my-avatar)
        'done))
```

```scheme
(define drop-thing! thing person)
  (move! thing (get-location person) person)
```

The following handler for generic-move! enables dropping a thing. The actor may be dropping a thing from its own bag or it might pick up something from another person's bag and drop it.

```scheme
(define-generic-procedure-handler generic-move!)
  (match-args mobile-thing? bag? place? person?)
  (lambda (mobile-thing from actor)
    (let ((former-holder (get-holder from)))
      (cond ((eqv? actor former-holder))
            (narrate! list actor)
                  "drops" mobile-thing
              actor)
            else (narrate! list actor)
                  "takes" mobile-thing
                  "from" former-holder
                  "and drops it"
                  actor)))
      (if (not eqv? actor former-holder)
        (say! former-holder)
        (list "What did you do that for?" from to)))
    (move-internal! mobile-thing from to))))
```

Another generic-move! handler provides for gifting or stealing, by moving a thing from one bag to another bag. Here the behavior depends on the relationships among the actor, the original holder of the thing, and the final holder of the thing.

```scheme
(define-generic-procedure-handler generic-move!)
  (match-args mobile-thing? bag? bag? person?)
  (lambda (mobile-thing from actor)
    (let ((former-holder (get-holder from)))
          (new-holder (get-holder to)))
      (cond ((eqv? (list new-holder "is already carrying"
                    mobile-thing)
            (tell! actor))))
```

```scheme
  ((eqv actor former-holder)
   (narrate! (list actor
             "gives" mobile-thing
             "to" new-holder)
             actor))
  ((eqv actor new-holder)
   (narrate! (list actor
               "takes" mobile-thing
               "from" former-holder)
             actor))
  (else
   (narrate! (list actor
               "takes" mobile-thing
               "from" former-holder
               "and gives it to" new-holder)
             actor))
  (if (not (eqv actor former-holder))
    (say! former-holder (list "Yaaah! I am upset!")))
    (if (not (eqv actor new-holder))
      (say! new-holder)
        (list "Whoa! Where'd you get this?")))
    (if (not (eqv from to))
      (move-internal! mobile-thing from to))))
```

Another interesting case is the motion of a person from one place to another. This is implemented by the following handler:

```scheme
(define-generic-procedure-handler generic-move!
  (match-args person? place? place?)
  (lambda (person from actor)
    (let ((exit (find-exit from) (get-heaven)))
      (cond (or (eqv from (get-heaven))
            (eqv to (get-heaven)))
            (move-internal! person from to))
          (not exit)
          (tell! (list "There is no exit from"
            "to" to)
            actor))
          ((eqv? person actor)
           (narrate! (list person "leaves via the"
                 (get-direction exit) "exit")
             from)
           (move-internal! person from to))
          (else
           (tell! (list "You can't force"
              person))))
"to move!)"
actor)))))
```

There can be many other handlers, but the important thing to see is that the behavior of the move procedure can depend on the types of all of the arguments. This provides a clean decomposition of the behavior into separately understandable chunks. It is rather difficult to achieve such an elegant decomposition in a traditional object-oriented design, because in such a design one must choose one of the arguments to be the principal dispatch center. Should it be the thing being moved? the source location? the target location? the actor? Any one will make the situation more complex than necessary.
As Alan Perlis wrote: "It is better to have 100 functions operate on one data structure than 10 data structures."

# Implementing properties

We saw that the objects in our game are created by defining some properties with make-property, defining a type predicate make-type, getting the predicate's associated instantiator with type-instantiator, and calling that instantiator with appropriate arguments. This simple description hides a complex implementation that is worth exploring.

The interesting aspect of this code is that it provides a simple and flexible mechanism for managing the properties that are associated with a type instance, which is robust when subtyping is used. Properties are represented by abstract objects rather than names, in order to avoid namespace conflicts when subtyping. For example, a mammal might have a property named forelimb that refers to a typical front leg. A subtype bat of mammal might have a property with the same name that refers to a different object, a wing! If the properties were specified by names, then one of those would need to change its name. In this implementation, the property objects are specified by themselves, and two properties with the same name are distinct.

The procedure make-property creates a data type containing a name, a predicate, and a default-value supplier. Its first argument is the property's name, and the rest of the arguments are a property list with additional metadata about the property. For example, see the

definition of troll:hunger on page 143. We will ignore how the property list is parsed since it's not interesting.

```scheme
(define (make-property name . plist)
  (guarantee:symbol? name)
  (guarantee property-list? plist)
  (%make-property name
    (get-predicate-property plist)
    (get-default-supplier plist)))
```

A property is implemented as a Scheme record [65], which is a data structure that consists of a set of named fields. It is defined by elaborate syntax that specifies a constructor, a type predicate, and an accessor for each field:

```scheme
(define-record-type <property>
  (%make-property name predicate default-supplier)
    property?)
  (name-property)
  (predicate-property)
  (default-supplier property-default-supplier))
```

We choose to give the primitive record constructor %-- an name sign initial initial often use the initial sign to the a low-level procedure that will not be except to support a higher-level abstraction. The %make-property procedure is used only in make-property, which in turn is used by other parts of the system.

Given a set of properties, we can construct a type predicate:

```scheme
(define (make-type name properties)
  (guarantee-list-of-properties properties)
  (let ((type
    (simple-abstract-predicate name instance-data?))
    (%set-type-properties! type properties))
  type))
```

A type predicate is an ordinary abstract predicate (see page 134) along with the specified properties, which are stored in an association using %set-type-properties!. Those specified properties aren't used by themselves; instead they are aggregated with the properties of the supersets of this type. The object being
