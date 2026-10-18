```
id("maven-publish")
```

And now to publish it locally, run on the terminal:

```
./gradlew shared-action:publishToMavenLocal
```

When the operation ends, you can read BUILD SUCCESSFUL in the console logs.

If you want to publish all your libraries locally, you should run instead:

```
./gradlew publishToMavenLocal
```

The default location for your local maven repository is on:

```
~/.m2/repository
```

Navigate to this folder, and you can see a com/raywenderlich/shared directory with the shared-action library for the different platforms inside.

Return to Android Studio. Before continuing, remove the include of the shared-action module from settings.gradle.kts:

```
include(":shared-action")
```

On the root of the learn project, open the build.gradle.kts. In the allprojects section, under repositories after google(), add:

```
mavenLocal()
```

The next time Gradle synchronizes, it will also look for the project dependencies in your .m2/repositories directory.

You’re just missing an update to the app’s dependencies. Open the build.gradle.kts files from androidApp and desktopApp and replace the entry:

```
implementation(project(":shared-action"))
```

that looks for the project, with: