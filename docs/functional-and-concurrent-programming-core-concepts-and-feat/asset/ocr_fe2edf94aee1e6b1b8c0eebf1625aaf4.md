closures, 130–134, 377. See also scoping
collections. See data structures
compare-and-set (CAS), 400–404, 414. See also atomic operations
composition
  of actions, 10–11
  of functions, 10–12
  of objects, 172, 231–232
comprehension
  for-comprehension, 35–37, 153–155, 212–213, 317, 362, 389, 407. See also higher-order functions
  list comprehension, 154–155
concat list function (::), 59, 85–86
condition synchronizer, 343–346, 354, 364–366. See also locks
cons (::), 31. See also functional lists
consumer. See producer-consumer pattern
contains list function, 80–81
contravariance, 238–240, 251–252. See also variance,
  annotation (-), 238–239
  restrictions on, 239
control abstraction, 176–179, 193
coroutines, 407, 412–413. See also async/await
count higher-order function, 138
countdown latch synchronizer, 325–328, 334, 339–340, 354
covariance, 222, 237–240, 244, 251–252. See also variance
  annotation (+), 237–239
  restrictions on, 238
currying, 5, 118–120, 134, 148. See also partial application
cyclic barrier synchronizer, 340–341, 354

D
daemon threads, 264, 313
data structures. See also functional lists; trees; streams; thread-safety
  lock-free, 401–404
  mutable versus immutable, 29–30
  parallel, 314–319, 362
  recursive, 6, 53–54, 61, 69–71
deadlocks, 259, 304–306, 325–327, 335–336, 342, 374, 382–383, 391,
  debugging with thread dumps, 328–329, 336
  of tasks and not threads, 412–415

default arguments. See arguments
defensive copies, 33–34, 37, 56, 289, 291, 296
domain specific language (DSL), 179, 194. See also control abstraction
drop list function, 82–84, 89
dropWhile higher-order function, 139
DSL. See domain specific language
duck typing. See structural subtyping
dynamic binding. See subtype polymorphism
dynamic dispatch. See subtype polymorphism

E
error handling. See failure handling
exceptions, 48, 177, 195–197, 199, 201–204
exists higher-order function, 137–138, 152, 164–165
expressions, 25–28, 36,
  code block as, 14
  if-then-else as, 10, 26, 28, 36
  statements versus, 25–26
  switch as, 28, 47, 60
extension methods, 13–14, 178, 247. See also methods
extractors, 59–61. See also pattern matching

F
failure handling, 6, 195–204
  of futures, 199, 374, 394–395
  using higher-order functions, 198, 200–204
filter, filterNot higher-order functions, 138, 142, 154–155
find higher-order function, 116–118, 167–168
flatMap higher-order function, 141–146, 153, 155, 211–213, 388–389, 393–394
flatten
  list function, 87
  on futures, 389
fold, foldLeft, foldRight higher-order functions, 146–148, 152, 155, 165–166
forall higher-order function, 137–138
foreach higher-order function, 140–141, 152–155