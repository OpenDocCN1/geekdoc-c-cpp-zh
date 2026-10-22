three files and a new directory to our application. That directory will contain the template files for the controller's views. In our case, we created a controller named say, so the views will be in the directory app/views/say.

To complete our “Hello, World!” application, let’s create a template. By default, Rails looks for templates in a file with the same name as the action it’s handling. In our case, that means we need to create a file called hello.html.erb⁷ in the directory app/views/say. (Why .html.erb? We’ll explain in a minute.) For now, let’s just put some basic HTML in there:

```
Download work/demo1/app/views/say/hello.html.erb
<html>
  <head>
    <title>Hello, Rails!</title>
  </head>
  <body>
    <h1>Hello from Rails!</h1>
  </body>
</html>
```

Save the file hello.html.erb, and refresh your browser window. You should see it display our friendly greeting. Notice that we didn’t have to restart the application to see the update. During development, Rails automatically integrates changes into the running application as you save files:

![](bbox=[0.18, 0.5, 0.58, 0.6])

So far, we’ve added code to two files in our Rails application tree. We added an action to the controller, and we created a template to display a page in the browser. These files live in standard locations in the Rails hierarchy: controllers go into app/controllers, and views go into subdirectories of app/views. This is shown in Figure 4.4, on the following page.

# Making It Dynamic

So far, our Rails application is pretty boring—it just displays a static page. To make it more dynamic, let’s have it show the current time each time it displays the page.

To do this, we need to make a change to the template file in the view—it now needs to include the time as a string. That raises two questions. First, how do we add dynamic content to a template? Second, where do we get the time from?

7. In prior versions of Rails, this file would have been called hello.rhtml.