# LISTING 6-132 A more general memoization function

```
let mem f =
  let lookup = System.Collections.Generic.Dictionary<, _>
fun n ->
  match lookup.TryGetValue n with
    | true, v -> v
    | _ ->
      let a = f n
      lookup.Add(n, a)
a
```

```
let rec fibonacci3 = mem (fun n)
  match n with
  | 0 | 1 -> 1
  | _ -> (fibonacci3 (n - 1) + (fibonacci3 (n - 2))
```

![](bbox=[0.093, 0.381, 0.133, 0.417])

Note Listing 6-132 generates a warning: "This and other recursive references to the object(s) being defined will be checked for initialization-soundness at runtime through the use of a delayed reference. This is because you are defining one or more recursive objects, rather than recursive functions. This warning might be suppressed by using '#nowarn "40'' or ''nowarn:40''. This is to prevent the user from writing the following code, which will generate a runtime exception:

```
let init f = f()
let rec foo = init (fun() -> foo : obj)
```

Listing 6-132 is not a template you can pass in any recursive function. Thanks to Uladimir on our team, a new version is shown in Listing 6-133.

# LISTING 6-133 Memoization code template

```
let memorize wrapFunction =
  let cache = System.Collections.Generic.Dictionary()
  let rec x =
    match cache.TryGetValue x with
    | true, v -> v
    | false, _ ->
      let v = wrapFunction f
      cache.[x] <- v
v
```