# 708 Surfing Web Streams

![](bbox=[0.238, 0.115, 0.863, 0.405])

**Figure 4-1**nThe initial request.

Now press <F10> until the Page_Load event is over, and Visual Studio returns control to your web browser. Notice that the Debug.WriteLine statement is never called. Why? ContentLength is 0. There is no Form request. (Kinds like “There is no spoon.") The content is empty, because it is an initial request. The Form collection is empty. Nothing is except the basic request information.

Press the button when the browser comes back. Visual Studio breaks again on the other foreach statement in the Button1_Click method. Put your mouse over the Request object again. Note the Form collection, shown in Figure 4-2. There are three items in it, the two hidden fields added by ASP-NET that you added, Button1.

This is the second type of request — the POST. It is in response to a form. This is where lot useful information can be found.