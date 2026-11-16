![](bbox=[0.153, 0.102, 0.576, 0.368])

Figure 4.17 Creating a WAR File in the Eclipse IDE: Part 2

After the server is up and running, you can trigger the deployment by using the deploy:local command, the syntax of which is illustrated in Listing 4.5. If all goes well, The Console Client will return with a message indicating that the application was deployed successfully. From here, you can test your results by opening the application in a web browser. Unless you explicitly changed the port configuration during the server installation process, the URL will be of the form http://localhost:8080/path/to/your/application.

```
neo deploy:local --source c:/users/james/desktop/example04_01.war
--location <target server directory>
```

Listing 4.5 Triggering a Local Deployment via the Console Client

# Triggering a Remote Deployment

To a large degree, the process of deploying to the cloud using the Console Client is quite similar to the one used to perform local deployments. Here, we collect our WAR file(s) as demonstrated in the previous section and then use the deploy command to trigger the deployment. The syntax for this command is demonstrated in Listing 4.6.

```
neo deploy --host <landscape_host> --account <account_name>
--application <application_name>
--source <path_to_war_file>
--user <email_or_user>
```

Listing 4.6 Syntax for Invoking the deploy Command