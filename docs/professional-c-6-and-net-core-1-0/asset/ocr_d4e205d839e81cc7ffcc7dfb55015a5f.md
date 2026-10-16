# Deployment as Part of the Application Life Cycle

The development process does not end when the source code is compiled and the testing is complete. At that stage, the job of getting the application into the user’s hands begins. Whether it’s an ASP.NET application, a WPF client application, or a Universal Windows Platform (UWP) app, the software must be deployed to a target environment.

Deployment should be considered very early in the design of the application, as this can influence the technology to be used for the application itself.

The .NET Framework has made deployment much easier than it was in the past. The pains of registering COM components and writing new hives to the registry have been eliminated.

This chapter looks at the options that are available for application deployment, from both a desktop client application (WPF) and UWP apps.

> NOTE Deployment of Web applications is covered in Chapter 45, “Deploying Websites and Services.”

# Planning for Deployment

Often, deployment is an afterthought in the development process that can lead to nasty, if not costly, surprises. To avoid grief in deployment scenarios, you should plan the deployment process during the initial design stage. Any special deployment considerations—such as server capacity, desktop security, or the location from which assemblies will be loaded—should be built into the design from the start, resulting in a much smoother deployment process.

Another issue that you should address early in the development process is the environment in which to test the deployment. Whereas unit testing of application code and deployment options can be done on the developer’s system, the deployment must be tested in an environment that resembles the target system. This is important to eliminate the dependencies that don’t exist on a targeted computer. An example of this might be a third-party library that has been installed on the developer’s computer early in the project. The target computer might not have this library on it. It can be easy to forget to include it in the deployment package. Testing on the developer’s system would not uncover the error because the library already exists. Documenting dependencies can help to eliminate this potential problem.

Deployment processes can be complex for a large application. Planning