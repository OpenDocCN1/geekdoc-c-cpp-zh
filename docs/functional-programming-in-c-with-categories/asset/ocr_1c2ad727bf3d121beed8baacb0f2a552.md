+   2. The next step is the .MapT(PersistCourse) bypass the Task and applies the function PersistCourse on the content of the Validation (which is a Course object) from the previous step using the Validation.Map method.
+   At this point the Type that we have at our hands after the PersistCourse is Validation<Error, Task<int>>

![](bbox=[0.12, 0.24, 0.88, 0.29])

[You can see the types at any given state by placing the cursor over the variable

```
2 references
public Task<Either<Error, int>> Handle(CreateCourse request, CancellationToken cancellationToken) =>
  Validate(request)
    .MapT(Persi Validation<Error, Task<int>> v
    .Bind(v => v.ToEitherAsync());
```

]

+   3. we want to convert this Validation<Error,Task<int>> into a Task<Either<Error,int>> that follows the usual pattern of responses so here is implemented an extension method for this purpose just to transfer the Task outside of the Validation and also convert the Validation to an Either using validation.ToEither()

```
public static Task<Either<Error, R>> ToEitherAsync<R>
    (this Validation<Error, Task<R>> validation) =>
        validation.ToEither()
        .MapLeft(errors => errors.Join())
        .MapAsync<Error, Task<R>, R>(e =>
    e);
```

And is applied through the .Bind(v => v.ToEitherAsync());

All the difficulty of this functional approach is concentrated on how to properly convert the types using the Map, and Bind and the various Transformation methods.

![](bbox=[0.13, 0.82, 0.85, 0.87])