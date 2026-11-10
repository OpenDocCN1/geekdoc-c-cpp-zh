+   3. In the next step, enter the name of the function module that should be offered as a web service. Because you initiated the wizard from the function module, the function module name should be prefilled. Select the MAP NAME checkbox (see Figure 19.83) to remove underscores in the function name and capitalize the first letter in each word (i.e., set it in camel case).

![](bbox=[0.148, 0.222, 0.857, 0.56])

**Figure 19.83** Endpoint Function Module

+   4. In the next step, select the security profile for the web service. This specifies how the authentication should be performed for the web service.
+   5. In the next step, select the package for the web service.
+   6. In the final step, click COMPLETE to create the web service. The system will take you to the web service definition, as shown in Figure 19.84. Activate the web service.
+   7. The web service doesn't have a runtime release at this point, so it can't be used. We can create the runtime release via Transaction SOAMANAGER.
+   8. Open Transaction SOAMANAGER to launch the SOA MANAGEMENT application in your web browser. Under the SERVICE ADMINISTRATION tab, click the SIMPLIFIED WEB SERVICE CONFIGURATION link, as shown in Figure 19.85.