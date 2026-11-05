![](bbox=[0.14, 0.11, 0.88, 0.6])

Figure 15-9 MainContent in the Default.aspx page

Here, in Figure 15-9 in addition to the static text "Welcome to ASP.NET!", two dynamic links were included in the MainContent ContentPlaceholder area. For the content pages shown in Figures 15-8 and 15-9, the line begins with <asp:Content, this is what ties the element back to the Site.master page.

As you review the DynamicPage Web application, you will discover additional content pages under the Account node. ChangePassword.aspx, ChangePasswordSuccess.aspx, Login.aspx, and Register.aspx are all associated with the Site.master master page.

As you closely review Figures 15-7 through 15-9, you will notice that there is a node named styles shown in the Solution Explorer window. It is expanded to reveal a file named Site.css. This is a style sheet. The file is automatically added to the project when a Visual Studio 2010 Web site is created.

# Cascading Style Sheet (CSS)

Beginning with Visual Studio 2008, support was provided for incorporating Cascading style sheets (CSS) into ASP.NET Web applications. CSS, like master pages, enable you to provide more consistency across pages on your Web site. They let you separate the actual content from how it is going to look. Before CSS, all of the presentational attributes, like sizes and colors of