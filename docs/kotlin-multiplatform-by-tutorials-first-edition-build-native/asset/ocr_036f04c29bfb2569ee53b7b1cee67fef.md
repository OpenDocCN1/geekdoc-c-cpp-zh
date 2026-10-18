You should go to each of these files and provide an instance of
RemindersRepository . What if the repository has its own dependencies?
And what if those dependencies have their dependencies as well? This is a rabbit
hole you want to avoid getting into!

You can provide all the dependencies yourself and no one can prevent you from
doing so. Off the record, iOS developers usually do all this and write all the
boilerplates by themselves, since there’s not a popular library or methodology
which everyone agrees on.

However, in the Android world, some libraries that solve this problem by
automating the process of creating and providing dependencies. They fall into
two categories:

+   Static solutions, which generate the dependency graph at compile time.

+   Solutions that connect the dependencies at runtime.

The most famous library for the first category is Dagger. Recently, Google
introduced Hilt, which they built on top of the foundations of Dagger. Google
recommends Hilt as part of their app architecture suggestions.

The catch is that neither Dagger nor Hilt is available for KMP. Thus, the
approach you can take is to do manual DI or use the most famous library of the
second category: Koin.

Many would call libraries like Koin — which resolve dependencies at runtime —
Service Locators. Those who favor static DI libraries will seriously object if you
call Koin a DI library. However, here you’re free to call it whatever you like.

# Setting up Koin

Setting up Koin is similar to how you’ve set up other multiplatform libraries in
the previous chapters - a shared part and some specific libraries to use for each
platform.

Open build.gradle.kts for the project and add a top-level constant for the Koin
version. As of writing, the latest version of Koin is 3.1.5.

```
val koinVersion by extra("3.1.5")
```

Next, open build.gradle.kts for the shared module.

Add a dependency for commonMain source set as follows: