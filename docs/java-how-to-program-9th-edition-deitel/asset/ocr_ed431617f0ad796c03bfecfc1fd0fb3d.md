# index.xhtml

The changes required to add Ajax functionality to this app are minimal. All of the changes are in the index.xhtml file (Fig. 30.12) and are highlighted. The ValidationBean class is identical to the version in Section 29.7, so we don’t show it here.

```
1 <?xml version='1.0' encoding='UTF-8' ?>
2
3 <!-- index.xhtml -->
4 <!-- Validating user input -->
5 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
6 "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
7 <html xmlns="http://www.w3.org/1999/xhtml"
8     xmlns:h="http://java.sun.com/jsf/html"
9     xmlns:f="http://java.sun.com/jsf/core">
10 <h:head>
11     <title>Validating Form Data</title>
12     <h:outputStylesheet name="style.css" library="css"/>
13 </h:head>
14 <h:body>
15     <h:form>
16         <h1>Please fill out the following form:</h1>
17         <p>All fields are required and must contain valid information</p>
18         <h:panelGrid columns="3">
19             <h:outputText value="Name:"/>
20             <h:inputText id="nameInputText" required="true"
21                 requiredMessage="Please enter your name"
22                 value="#{validationBean.name}"
23                 validatorMessage="Name must be fewer than 30 characters">
24                 <f:validateLength maximum="30" />
25             </h:inputText>
26             <h:message id="nameMessage" for="nameInputText"
27                 styleClass="error"/>
28             <h:outputText value="E-mail:"/>
29             <h:inputText id="emailInputText" required="true"
30                 requiredMessage="Please enter a valid e-mail address"
31                 value="#{validationBean.email}"
32                 validatorMessage="Invalid e-mail address format">
33                 <f:validateRegex pattern=
34                     "\w+([.+']\w+)*@\w+([-. ]\w+)*\.\w+([-. ]\w+)*" />
35             </h:inputText>
36             <h:message id="emailMessage" for="emailInputText"
37                 styleClass="error"/>
38             <h:outputText value="Phone:"/>
39             <h:inputText id="phoneInputText" required="true"
40                 requiredMessage="Please enter a valid phone number"
41                 value="#{validationBean.phone}"
42                 validatorMessage="Invalid phone number format">
43                 <f:validateRegex pattern=
44                     "((\(\d{3}\) ?)|\d{3}-)?\d{3}-\d{4}" />
45             </h:inputText>
46             <h:message id="phoneMessage" for="phoneInputText"
47                 styleClass="error"/>
48         </h:panelGrid>
```