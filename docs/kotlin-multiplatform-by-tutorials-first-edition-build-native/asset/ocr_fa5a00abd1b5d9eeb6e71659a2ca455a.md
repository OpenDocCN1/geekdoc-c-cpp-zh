```
val viewModels = module {
    factory { RemindersViewModel(get()) }
    factory { AboutViewModel(get()) }
}
```

Declare to Koin how to resolve the dependency of the <o>AboutViewModel</o> class, which is of type <o>Platform</o> . Create a constant called <o>core</o> inside the <o>Modules</o> object to hold this and some other dependencies, which will come in a later chapter.

```
object Modules {
    val core = module {
    factory { Platform() }
    }
    // ...
}
```

Last but not least in this file, update the definition of <o>initKoin</o> to accept the new modules you defined:

```
fun initKoin(
    appModule: Module = module { },
    coreModule: Module = Modules.core,
    repositoriesModule: Module = Modules.repositories,
    viewModelsModule: Module = Modules.viewModels,
) : KoinApplication = startKoin {
    modules(
    appModule,
    coreModule,
    repositoriesModule,
    viewModelsModule,
    )
}
```

To follow the usual approach, you’ll next update the codes for the platforms in order.

# Android

Open <o>AndroidView.kt</o> in the <o>androidApp</o> module and change the <o>AboutView</o> composable definition to this:

```
fun AboutView(
    viewModel: AboutViewModel = getViewModel(),
    onUpButtonClick: () -> Unit
) { // ...
}
```