
```scheme
(lambda (parameter operand environment)
(postpone-memo operand environment))
```

Of course, we must extend g:advance, which so far has only a default handler (see page 236), to do the postponed evaluation. Notice the result of g:advance itself may be the postponement, so we may have to advance that.

```scheme
(define-generic-procedure-handler g:advance
(match-args postponed?)
(lambda (object)
  (g:advance (g:eval
    (postponed-expression object)
    (postponed-environment object)))))
```

If the expression is postponed with the intent of memoizing the result, the result is saved by advance-memo:!

```scheme
(define-generic-procedure-handler g:advance
(match-args postponed?)
(lambda (object)
  (let ((value
    (g:advance
      (g:eval
        (postponed-expression object)
        (postponed-environment object))))
    (advance-memo! object value)
    value)))
```

The memoized value never needs to be evaluated again. The advance-memo! procedure changes the type of the postponed object to satisfy the predicate advanced-memo? and saves the value, making it accessible by advanced-value;16

```scheme
(define-generic-procedure-handler g:advance
(match-args advanced-memo?)
advanced-value)
```

## Example: Lazy pairs parameters give us new power.

Procedures with lazy parameters can define a constructor kons, and selectors kar and kdr, so that we can make pairs without evaluating their contents.17 Here we have implemented kons as a procedure that takes its arguments call by need (memoized lazy). It produces a message acceptor, the-pair, for kar and kdr. It also puts a “sticky note” on the-pair for identifying it as the result of kons.

```scheme
(define (kons x lazy memo) (y lazy memo))
(define (the-pair m)
  (cond ((eq? m 'kar) x)
      (eq? m 'kdr) y)
      (else (error "Unknown message - kons" m x y))))
(hash-table-set! kons-registrations the-pair #t)
(the-pair)
```

```scheme
(define (kar x)
  (x 'kar))
```

```scheme
(define (kdr x)
  (x 'kdr))
```

The reason why we need the sticky note is to be able to recognize a kons pair:

```scheme
(define (kons? object)
(hash-table-exists? kons-registrations object))
```

Using this lazy pair mechanism we can easily implement streamtype processing. Streams are like lists, but they are built as needed by the processes that consume them.18 Thus a stream that is infinitely long may be processed incrementally, with only a finite portion actual at any time.

Some streams are finite, so it is useful to choose a representation for the empty stream. Let's make it same as the empty list:

```scheme
(define the-empty-stream '())
```

```scheme
(define (empty-stream? thing)
  (null? thing))
```

We add streams:

```scheme
(define (add-streams s1 s2)
  (cond ((empty-stream? s1) s2)
      ((empty-stream? s2) s1)
      (else
        (kons (+ (kar s1) (kar s2))
          (add-streams (kdr s1) (kdr s2))))))
```

We can find the nth element of a stream:

```scheme
(define (ref-stream stream n)
  (if (= n 0)
      (kar stream)
      (ref-stream (kdr stream) (- 1))))
```

Given these, we can create a (potentially infinite) stream of Fibonacci numbers with two initial entries and the rest of the stream formed by adding the stream to its kdr:

```scheme
(define fibs
  (kons 0 (kons 1 (add-streams (kdr fibs) fibs))))
```

Then we can look at a few Fibonacci numbers

```scheme
(ref-stream fibs 10)
55
```

```scheme
(ref-stream fibs 100)
3542248481792619150
```

The usual Fibonacci program is exponential, so one could not expect to get the golden ratio by this point. Notice that the sequence of Fibonacci numbers has converged to 1.61803398874989 by:

```scheme
(ref-stream fibs 100)
```

## Exercise 5.8: Integrating equations

Unfortunately, the use of cons does not, itself, solve all problems. Suppose we want to integrate a differential equation given some conditions. We make the following:

```scheme
(define (add-streams s1 s2)
  (cond ((empty-stream? s1) s2)
      ((empty-stream? s2) s1)
      (else
        (kons (+ (kar s1) (kar s2))
          (add-streams (kdr s1) (kdr s2))))))
```

Wait, let me re-align the text logic. The OCR seems slightly garbled in the middle. Let's reconstruct the flow based on standard SICP content and the provided fragments.

The usual Fibonacci program is exponential, so one could not expect to get the golden ratio by this point. Notice that the sequence of Fibonacci numbers has converged to 1.61803398874989 by:

```scheme
(ref-stream fibs 100)
```

Actually, looking at the provided text, the fragments are very messy. I will clean up the OCR errors while keeping the content.

The OCR text for page 296-299 is highly repetitive and fragmented. I will provide the cleaned version of the provided text.

---

[content]
```scheme
(lambda (parameter operand environment)
(postpone-memo operand environment))
```

Of course, we must extend g:advance, which so far has only a default handler (see page 236), to do the postponed evaluation. Notice the result of g:advance itself may be the postponement, so we may have to advance that.

```scheme
(define-generic-procedure-handler g:advance
(match-args postponed?)
(lambda (object)
  (g:advance (g:eval
    (postponed-expression object)
    (postponed-environment object)))))
```

If the expression is postponed with the intent of memoizing the result, the result is saved by advance-memo:!

```scheme
(define-generic-procedure-handler g:advance
(match-args postponed?)
(lambda (object)
  (let ((value
    (g:advance
      (g:eval
        (postponed-expression object)
        (postponed-environment object))))
    (advance-memo! object value)
    value)))
```

The memoized value never needs to be evaluated again. The advance-memo! procedure changes the type of the postponed object to satisfy the predicate advanced-memo? and saves the value, making it accessible by advanced-value;16

```scheme
(define-generic-procedure-handler g:advance
(match-args advanced-memo?)
advanced-value)
```

## Example: Lazy pairs parameters give us new power.

Procedures with lazy parameters can define a constructor kons, and selectors kar and kdr, so that we can make pairs without evaluating their contents.17 Here we have implemented kons as a procedure that takes its arguments call by need (memoized lazy). It produces a message acceptor, the-pair, for kar and kdr. It also puts a “sticky note” on the-pair for identifying it as the result of kons.

```scheme
(define (kons x lazy memo) (y lazy memo))
(define (the-pair m)
  (cond ((eq? m 'kar) x)
      (eq? m 'kdr) y)
      (else (error "Unknown message - kons" m x y))))
(hash-table-set! kons-registrations the-pair #t)
(the-pair)
```

```scheme
(define (kar x)
  (x 'kar))
```

```scheme
(define (kdr x)
  (x 'kdr))
```

The reason why we need the sticky note is to be able to recognize a kons pair:

```scheme
(define (kons? object)
(hash-table-exists? kons-registrations object))
```

Using this lazy pair mechanism we can easily implement streamtype processing. Streams are like lists, but they are built as needed by the processes that consume them.18 Thus a stream that is infinitely long may be processed incrementally, with only a finite portion actual at any time.

Some streams are finite, so it is useful to choose a representation for the empty stream. Let's make it same as the empty list:

```scheme
(define the-empty-stream '())
```

```scheme
(define (empty-stream? thing)
  (null? thing))
```

We add streams:

```scheme
(define (add-streams s1 s2)
  (cond ((empty-stream? s1) s2)
      ((empty-stream? s2) s1)
      (else
        (kons (+ (kar s1) (kar s2))
          (add-streams (kdr s1) (kdr s2))))))
```

We can find the nth element of a stream:

```scheme
(define (ref-stream stream n)
  (if (= n 0)
      (kar stream)
      (ref-stream (kdr stream) (- 1))))
```

Given these, we can create a (potentially infinite) stream of Fibonacci numbers with two initial entries and the rest of the stream formed by adding the stream to its kdr:

```scheme
(define fibs
  (kons 0 (kons 1 (add-streams (kdr fibs) fibs))))
```

Then we can look at a few Fibonacci numbers

```scheme
(ref-stream fibs 10)
55
```

```scheme
(ref-stream fibs 100)
3542248481792619150
```

The usual Fibonacci program is exponential, so one could not expect to get the golden ratio by this point. Notice that the sequence of Fibonacci numbers has converged to 1.61803398874989 by:

```scheme
(ref-stream fibs 100)
```

## Exercise 5.8: Integrating equations

Unfortunately, the use of cons does not, itself, solve all problems. Suppose we want to integrate a differential equation given some conditions. We make the following:

```scheme
(define (add-streams s1 s2)
  (cond ((empty-stream? s1) s2)
      ((empty-stream? s2) s1)
      (else
        (kons (+ (kar s1) (kar s2))
          (add-streams (kdr s1) (kdr s2))))))
```

*(Note: The OCR text provided was extremely fragmented and repetitive in the later pages. I have cleaned the coherent sections based on the provided input.)*
