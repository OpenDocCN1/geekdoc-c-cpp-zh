# BEWARE LOADING DIALOGS

Remember that mobile applications are not like their web or desktop counterparts. Your users will typically be using their phones when they’re away from a conventional computer. This means, usually, that they’re already waiting for something: a bus, that cup of expensive coffee, their friend to come back from the bathroom, or a boring meeting to end. It’s very important, therefore, to keep them from having to wait on anything within your application. Waiting for your mobile application to connect while you’re already waiting for something else can be a frustrating experience. Do what you can to limit users’ exposure to full-screen loading dialogs. They’re unavoidable sometimes, but minimize them whenever possible.

# SHOWING YOUR PROGRESS

There’s another aspect of the AsyncTask that you should be aware of even though I haven’t demonstrated it. From within doInBackground, you can send progress updates to the user interface. doInBackground isn’t on the main thread, so if you’d like to update a progress bar or change the state of something on the screen, you’ll have to get back on the main thread to make the change.

Within the AsyncTask, you can do this during the doInBackground method by calling publishProgress and passing in any number of objects deriving from the second class in the AsyncTask declaration (in the case of this example, an integer). Android will then, on the main thread, call your declared onProgressUpdate method and hand over any classes you passed to publishProgress. Here’s what the method looks like in the AsyncTask example:

```
```java
protected void onProgressUpdate(Integer... params){
    //Update a progress bar here, or ignore it, it's up to you
}
```
```

As always, be careful when doing UI updates, because if the activity isn’t currently onscreen or has been destroyed, you could run into some trouble.