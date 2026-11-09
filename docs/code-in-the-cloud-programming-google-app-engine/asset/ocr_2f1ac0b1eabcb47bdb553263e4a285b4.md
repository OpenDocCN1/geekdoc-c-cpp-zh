makes it easy to reuse this script. If we just executed run_wsgi_app directly, then if we were to import this script into any other Python code, that line would be executed. The main function plus the conditional invocation ensures that we’ll only execute it if we specifically run this script—it won’t be executed by modules that import this.

We can deploy the new version of this exactly the same way as the last one. I changed the filename of the Python script, so I needed to also update the app.yaml file to reference the new Python script file. Once that’s done, deployment is done by just running appcfg.py update chotane. That will upload the changes. Immediately after running the update, go to the application URL, which will run the new version of the code. It will still appear in Google App Engine as version 1, because I didn’t change the version identifier in app.yaml.

This quick and dirty explanation just gives you a sense of what developing for Google App Engine is like. In later chapters, we’ll look at all of the aspects of developing interesting web applications in App Engine in greater detail.

# 2.4 Monitoring Your Application

As the developer of an application, you’ll want to monitor it—to be able to detect how many users you have, the quantity of resources being consumed, the number of hits, which scripts are most active, what’s working, what isn’t, and so on. You can do that by using the Google App Engine control panel.

The monitoring features of the Google App Engine control panel is going to be really important for you. Your cloud application is running on a computer that you don’t control. You can’t just run a profiler or a debugger to try to see why things aren’t working the way you expect. So when you find that something is taking much longer than you think it should (and that’s something that will eventually happen if you write any serious cloud applications), the monitor is your information source.

As an example, in my day job, I build cloud-based data analysis applications for Google. I’ve had cases where an analysis that usually runs for one hour suddenly started taking eight hours. That’s obviously a really bad thing. I was able to figure out what was going on by going into the control panel, looking at the information it could give me, and