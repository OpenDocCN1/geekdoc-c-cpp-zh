side effect of marshaling the data across to the thread containing the form. In this case, InvokeRequired is false, and you can retrieve the data from the workflow. Figure C-13 shows the result.

Combining ASP.NET with Windows Workflow Foundation raises many of the same issues involved in using WF with other technologies. That is, you still need to host the services and the runtime of WF within the host process under which ASP.NET runs — within IIS. However, developing solutions using ASP.NET offers more features and requires more decisions than other solutions. In particular, it is possible to publish workflows as ASP.NET Web services. Hosting workflows within ASP.NET solutions is similar to hosting workflows with Windows Forms, but an ASP.NET solution might actually be supporting multiple concurrent users. This means that you must be more aware of where the runtime is created and how instances are created and freed.

You can host a workflow as a Web service if it has one or more WebServiceInput activities. This activity represents a SOAP endpoint. The WebServiceInput activity needs two properties set: InterfaceType and MethodName. Communication between the client code and the Web service is achieved via a shared interface. This interface is the value needed for the InterfaceType property. It represents the contract between the client code and the WebServiceInput activity. The MethodName identifies the method on the interface that will initiate the Web service call. The first WebServiceInput activity should have the IsActivating property set to true. In addition to the WebServiceInput activity, the workflow should also include a WebServiceOutput activity if the method includes a return value. Including a WebServiceFault activity is also useful if you need to return an error to the client code. If the Web service has parameters or return values, these may be mapped to the properties of the workflow using the Bind property dialog (see Figure C-14). Open this dialog by clicking the ellipsis next to the property in the Properties window.

Once you have built the workflow, including the WebServiceInput and WebServiceOutput activities (see Figure C-15), you then publish it as a Web service. This adds an additional ASP.NET Web Service project to the solution. The wizard creates the ASMX file that wraps the workflow and adds the required settings to the web.config file. The ASMX wrapper does nothing but delegate to the workflow class.

```
<%@WebService Class="TranslateService.TranslateWorkflow_WebService" %>
```

![](bbox=[0.52, 0.09, 0.88, 0.25])

# FIGURE C-13

![](bbox=[0.09, 0.69, 0.49, 0.93])

# FIGURE C-14

![](bbox=[0.54, 0.61, 0.88, 0.93])

# FIGURE C-15