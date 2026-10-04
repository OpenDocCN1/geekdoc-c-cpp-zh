
# 17
## Personalizing Websites

WHAT YOU WILL LEARN IN THIS CHAPTER:

- Details about the Profile feature that ships with ASP.NET
- How to create and consume a user's profile in a website
- How you can recognize your users and how to serve them customized content
- How you can access the profile of other users of your site

WROX.COM DOWNLOADS FOR THIS CHAPTER

You can find the wrox.com code for this chapter on the Download Code tab at www.wrox.com/go/begaspnet451. The code is in the Chapter 17 folder.

There is only one thing that beats good content on the web — *personalized* content. In the era of information overload and the huge amount of competitive sites, it's important to know your visitors and understand the possibilities to present them personalized content. With a good personalization strategy, you can create a website that lives up to your users' expectations by presenting them with exactly the data they are looking for. Personalization is useful for many different scenarios. For example, on a sports site, you use personalized content to highlight activities from the user's favorite team. On a site that deals with programming, you can personalize content by showing users examples in their preferred programming language(s) only. On a news website, you can let users choose one or more news categories (World, Local, Sports, Business, Financial, and so on) and target the content you show them based on these preferences. You can take this one step further by sending them e-mail updates when a new article is posted in one of those categories.

However, personalization goes further than just storing personal preferences and adapting the content to these preferences. With personalization, you can also keep track of other user details, such as a name, date of birth, visits to the site, items users bought in an online shop, and so on. You can then use these details to further personalize web pages, creating a closer relationship with your visitors.

In the Planet Wrox website, personalization is implemented simply yet effectively. The Main Reviews page is designed to show only the reviews for music genres in which the user is interested. To see all the available reviews, users can still visit the reviews in genres A1.aspx page; by visiting the personalized page, they only see reviews they really like.

Additionally, users can enter personal details about themselves, such as a first and last name, and a short biography. These details are shown on the Photo Albums details page some you know created a particular photo album.

To enable you to add personalization features to a website, ASP.NET 4.5.1 ships with an application called Profile. With the Profile service, you can store data for a particular user with very few lines of code.

By the end of this chapter, you'll have enough knowledge about the personalization features brought by Profile to create dynamic and personalized websites.

## UNDERSTANDING PROFILE

The ASP.NET Profile is another application service that ships with ASP.NET. It enables you to store and retrieve information about your users that goes beyond basic information such as an e-mail address and password that users can enter during sign-up. With Profile, you can store information such as a first and last name, date of birth, and month, as you see later in this chapter. Keeping track of the user to that data belongs, ASP.NET is able to map that data to a user the next time she visits your site, whether that is minutes or weeks later. The cool thing about Profile is that it enables you to store data for registered users as well as anonymous users. So, if your visitors haven't signed up for an account, you can recognize them and store information about them.

You access the information in a user's profile through a clean API with virtually no code. All you need to do is define the information you want to keep track of in the Web.config file and the Profile service takes care of the rest. All interaction with the database to retrieve or store profile information in the database is handled automatically for you.

Enabling Profile in your web application is a, two-step process:

1. Define the information you want to store for a user in the Web.config file. Based on this information, the ASP.NET run time generates and compiles a class for you on the fly that gives you access to the properties you defined. It dynamically expands a property called Profile on all web pages in your site, you can easily access the profile properties from every page in your site.

2. In your application, program directly to this generated class to get and store the profile information for the current user.

The ASP.NET Profile by default is connected to a logged-in user, although you can also save profile data for unauthenticated users, as you will see later in this chapter.

In the following section, you see how to define profile properties in Web.config and how to access them in your web pages.

> NOTE It's important to realize that the built-in Profile feature works only with Web Site Projects and not with Web Application Projects. For a discussion on the difference between the two, refer to Chapter 2. If you find that none of the examples in this chapter seem to work, check that you have accidentally created a Web Application Project. The simplest way to check is at the Code Behind file of a Web Form. If you see two Code Behind files (one named after the page with .cs or .vb extension and one with an additional Designer extension), you have created a Web Application Project. In that case, get yourself a copy of the folder that is part of the source that comes with this and use that as the starting point for this chapter.

## Configuring the Profile

You define a profile for your website in the Web.config file by creating a profile element.

### Creating Simple Properties

You define a profile for your website in the Web.config file by creating a profile element. The following table lists the most common attributes of the <add> element that influence the properties.

| ATTRIBUTE | DESCRIPTION |
| :--- | :--- |
| name | Defines the name of the property, such as FirstName, DateOfBirth. |
| type | Sets the full .NET name of the property, such as System.String, System.Boolean, System.DateTime, System.Int32. |
| allowAnonymous | Specifies whether the property can be written to for anonymous users. The default is false. |
| defaultValue | Defines the default value for the property if it hasn't been set explicitly. |
| readOnly | Specifies whether the profile property can be changed at run time. The default is false. |

Besides simple properties, you can also create group properties that enable you to group other simple properties together.

Profile groups serve two distinct purposes: first, to enable you to logically group related properties. For example, you can create a group called Address that, in turn, has properties like Street, PostalCode, and City.

Groups also enable you to have properties with the same name, but in a different group. For example, you can have groups VisitAddress and PostalAddress that both feature properties like Street and PostalCode, making it easier for a developer using your Profile object to find the relevant information.
