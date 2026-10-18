![](bbox=[0.386, 0.062, 0.614, 0.359])

You haven’t changed the UI yet, but this makes sure the Gradle files are still working.

# ## Find Time

Have you ever needed to schedule a meeting with colleagues who work in different time zones? It can be a real pain. Are they awake at the hour you want to schedule? What are good times to schedule a meeting? You’re going to write the Find Time app to help find those hours that work best. To do that, you need to write some time zone logic to figure out the best hours to meet. If you were to write separate apps for iOS and Android, you would have to write that business logic twice.

# ## Business logic

One of the main benefits of KMP is you can share business logic among all your platforms. You’ll write your business logic in the shared module. This module is a multiplatform module you can use for iOS, Android, desktop and the web.

Open the shared/src folder and then androidMain, commonMain and iosMain folders. You’ll find the Platform and Greeting classes. Delete these classes as you won’t use them. Note that both the Android and iOS platforms won’t run until you delete the code that called them. Android Studio will complain about their usages. Click the View Usages button.