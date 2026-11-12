This method call does two things of note. First, it creates a new custom Twitter JSONAdapter, which I’ll show you how to create in a minute. Second, it creates a TwitterAsyncTask and fires it off.

You’ll have noticed, if you were watching closely, that I created a private data member to contain the Twitter-fetching task. You astute readers might be wondering why I chose to stash it aside that way. The answer is that because this task isn't happening on the main thread, I need to be able to cancel it should the user close down the activity before the task finishes. To do this, the onStop method will need to be able to call the Twitter-fetching AsyncTask, making it a private data member.

# ## GETTING TWITTER DATA

My first task, at least when it comes to doing work, is to load the stream of Twitter messages. You should, thanks to the previous chapter, be very familiar with the ins and outs of fetching network data. Thanks to your amazing proficiency, I’m going to hide the code required to do a network call and read it into a string. If you’re having trouble remembering how to do this, feel free to check out the sample code. Without further preamble, here’s what my TwitterAsyncTask looks like:

```
```java
private class TwitterAsyncTask extends
    AsyncTask<String, Integer, JSONArray>{
    @Override
    protected JSONArray doInBackground(String... params) {
        String response = getURLContents(params[0]);
        try {
            return new JSONArray(response);
        } catch (JSONException ex) { return null; }
    }
}
```
```