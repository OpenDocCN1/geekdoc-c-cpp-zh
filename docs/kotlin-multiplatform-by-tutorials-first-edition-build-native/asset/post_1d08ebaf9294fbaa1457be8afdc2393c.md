
# 13 Concurrency

*Written by Carlos Mota*

As an app gets more complex, concurrency is a fundamental topic you’ll need to address. **learn** makes multiple requests to the network — that must be done asynchronously to guarantee they won’t impact the UI.

> **Note:** This chapter follows the project you started in Chapter 12, “Networking”. Or, you can use this chapter’s starter project.

Here’s what you’ll do in this chapter:

- You’ll learn what coroutines are and how you can implement them.
- You’ll enable the new Kotlin/Native memory model.

## The need for structured concurrency

Structured concurrency allows doing multiple computations outside the UI-thread to keep the app as responsive as possible. It differs from concurrency in the sense that a task can only run within the scope of its parent, which cannot end before all of its children.

![](img/2f50555a40af4ea8c85f09e577f0c5b9_281_0.png)

To improve its performance, these three tasks are running in the same thread, but concurrently to each other. They were divided into smaller segments that run independently.

Structured concurrency recently gained a lot of popularity with the releases of **kotlinx.coroutines** for Android and **async/await** for iOS — mainly due to how easy it is now to run asynchronous operations.

## Different concurrency solutions

There’s a set of libraries built for Kotlin Multiplatform that support concurrency:

- **kotlinx.coroutines**: The most popular one, mostly because of its use among Android developers and recommendation from JetBrains and Google. It’s lightweight, it allows running multiple coroutines in a single thread and it supports exception handling and cancellation.
- **Reaktive**: An implementation of Reactive Extensions using the **Observable** pattern.
- **CoroutineWorker**: Supports multithreaded coroutines.

In this chapter, you’ll learn how to use **kotlinx.coroutines**. Spoiler alert: You’ve already worked with coroutines before. ;]

If you’re already familiar with coroutines, you can skip the next few sections and go to “Structured concurrency in iOS”, or directly to “Working with kotlinx.coroutines”, for the next developments in **learn**.

## Understanding kotlinx.coroutines

**Ktor** uses coroutines to make network requests without blocking the UI-thread, so you’ve already used them unwittingly in the previous chapter.

Open the **FeedPresenter.kt** file from **shared/commonMain/presentation** and search for `fetchAllFeeds` and `fetchFeed`. In the first function, you’ve got:

```kotlin
for (feed in content) {
  fetchFeed(feed.platform, feed.url)
}
```

If you weren’t using coroutines on `fetchFeed`, these instructions would run sequentially. In other words, the app would only iterate to the next item after `fetchFeed` returned, which would delay the app startup.

## Suspend functions

**Suspend functions** are at the core of coroutines. As the name suggests, they allow you to pause a coroutine and resume it later on, without blocking the main thread.

Network requests are one of the use cases for **suspend functions**. Open the **FeedAPI.kt** file on **shared/commonMain/data** and look at the functions’ declaration:

```
public suspend fun fetchRWEntry(feedUrl: String): HttpResponse =
client.get(feedUrl)

public suspend fun fetchMyGravatar(hash: String): GravatarProfile =
  client.get("$GRAVATAR_URL$hash$GRAVATAR_RESPONSE_FORMAT") {
    header(X_APP_NAME, APP_NAME)
  }.body()
```

They’re all **suspend functions**. Since a response may take some time, the app cannot block and wait for any of these functions to return.

This image defines the flow that triggers `fetchRWEntry` to be called.

![](img/2f50555a40af4ea8c85f09e577f0c5b9_283_0.png)

Fig. 13.2 - Diagram showing the different steps of a network request with coroutines.

The entry point, for all platforms, is the `fetchAllFeeds` function from **shared/commonMain/presentation/FeedPresenter.kt**. Once invoked, it iterates over all the RSS feeds, and calls `fetchFeed` for each one of its URLs:

[PAGE 284]

- This is a heavy operation that might block the UI. To avoid this, you’ll do it asynchronously. Create a coroutine by calling `launch`.
- Once launched, it calls `invokeFetchRWEntry` from **shared/commonMain/domain/GetFeedData.kt**. A **suspend function** calls the **FeedAPI** to make the request.
- This function suspends after making the request, and it waits until there’s a response or the connection times out.
- This is done in a separate thread, so the UI doesn’t get blocked.
- Once there’s a response, `fetchRWEntry` resumes and returns to `invokeFetchRWEntry`, which can now deserialize the information received.
- When this process finishes, the `onSuccess` or the `onFailure` functions execute — depending on the result — and the UI receives an update. Since you’re using `MainScope` to `launch` the coroutine, this means it will run on the UI-thread. You’ll see this in detail in the next section.

As a key point, you can only call a **suspend function** from another one or within a coroutine.

## Coroutine scope and context

Return to **FeedPresenter.kt** from **shared/commonMain/presentation** and search for the `fetchFeed` function:

```
private fun fetchFeed(platform: PLATFORM, feedUrl: String, cb: FeedData) {
    MainScope().launch {
        // Call to invokeFetchRWEntry
    }
}
```

You already know that `launch` creates a new coroutine, but what’s `MainScope`? A **coroutine scope** is where a coroutine is going to run — in this case, it will be the main thread.

If you open the source code of `MainScope`:

```
public fun MainScope(): CoroutineScope =
ContextScope(SupervisorJob() + Dispatchers.Main)
```

You can see that its `ContextScope` is built using:

- `SupervisorJob`: When you create a coroutine, it returns a `Job` that corresponds to its instance. This allows you to cancel or to know more about

[PAGE 285]

its current state:

- isActive : If it's currently running.
- isCompleted : If all of its work, as well as its children, have ended. Moreover, when the current Job gets cancelled — or fails — its value will be true.
- isCancelled : When the current job gets cancelled or fails.

The difference between a SupervisorJob and a Job is that they have different policies. In the first one, the children behave independently — if one fails, the others won't be affected — whereas in the second one, if a parent fails, all of its children will be cancelled.

- Dispatchers : Define in which thread a coroutine should run:

- Default : Uses a shared pool of threads.
- Main : Has different behaviors depending on the platform that's currently running. On JVM and Android, Main corresponds to the UI-thread, and should only be used for operations that update the UI. On Native, it's the same as the Default dispatcher.
- Unconfined : Doesn't have any associated threading policy. Doesn't switch to any specific thread.
- IO : Should be used for long-running and heavy tasks because it's one shared pool of threads, optimized for these types of operations. It's currently not available for iOS.

When you create a coroutine, you have to define the dispatcher where it should run, but you can always switch the context later on its execution by calling withContext with the prepended Dispatcher as an argument.

In the fetchMyGravatar function from FeedPresenter.kt, you're running the coroutine in the main thread, although the only part that is necessary to run are the onSuccess and onFailure calls. You can update the existing function to use the Default thread for the network requests and when the data is available, switch to the Main thread so the UI can be updated:

```
public fun fetchMyGravatar(cb: FeedData) {
    //1
    CoroutineScope(Dispatchers.Default).launch {
    //2
    val profile = feed.invokeGetMyGravatar(
        hash = md5(GRAVATAR_EMAIL)
    )

    //3
    withContext(Dispatchers.Main) {
}
```
