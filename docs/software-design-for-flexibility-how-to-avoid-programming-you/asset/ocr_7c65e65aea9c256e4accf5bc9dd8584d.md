for kar and kdr. It also puts a “sticky note” on the-pair for identifying it as the result of kons.

```
(define (kons x lazy memo) (y lazy memo))
(define (the-pair m)
  (cond ((eq? m 'kar) x)
      (eq? m 'kdr) y)
      (else (error "Unknown message - kons" m x y))))
(hash-table-set! kons-registrations the-pair #t)
(the-pair)
```

```
(define (kar x)
  (x 'kar))
```

```
(define (kdr x)
  (x 'kdr))
```

The reason why we need the sticky note is to be able to recognize a kons pair:

```
(define (kons? object)
(hash-table-exists? kons-registrations object))
```

Using this lazy pair mechanism we can easily implement streamtype processing. Streams are like lists, but they are built as needed by the processes that consume them.18 Thus a stream that is infinitely long may be processed incrementally, with only a finite portion actual at any time.

Some streams are finite, so it is useful to choose a representation for the empty stream. Let's make it same as the empty list:

```
(define the-empty-stream '())
```

```
(define (empty-stream? thing)
  (null? thing))
```

We add streams:

```
(define (add-streams s1 s2)
  (cond ((empty-stream? s1) s2)
      ((empty-stream? s2) s1)
      (else
        (kons (+ (kar s1) (kar s2))
          (add-streams (kdr s1) (kdr s2))))))
```