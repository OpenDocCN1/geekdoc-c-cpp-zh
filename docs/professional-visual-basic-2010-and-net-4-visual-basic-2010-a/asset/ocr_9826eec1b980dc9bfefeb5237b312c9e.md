# 20

# Silverlight and Services

# WHAT YOU WILL LEARN IN THIS CHAPTER

+   > ASMX Web Service
+   > ADO.NET Data Service
+   > WCF Ria Services
+   > Model-View-ViewModel

As you have seen in the previous chapter, Silverlight offers developers a familiar environment for developing applications. However, Silverlight offers a lot more than the capability to make great-looking websites. Silverlight has a rich line-of-business applications too. With Silverlight 3, Microsoft enabled developers to easily create a variety of business applications, including new DataForm controls and Validation controls. Silverlight 4, now in beta and soon to be released, will continue to strengthen Silverlight’s line-of-business support by adding additional features such as trusted offline capabilities and finer control on the offline.

Throughout this chapter you will learn both how to leverage existing Web service technologies and how to use some of the newer technologies targeted toward Silverlight. As with all line-of-business applications, it is important to be able to get to data and then update it back on the server. Silverlight can do this through existing Web services like SOAP or WCF with little modification, or you can use some of the new offerings of ADO.NET Data Services and RIA Services.

This chapter also offers a high-level overview of a commonly suggested best practice for developing Silverlight line-of-business applications called Model-View-ViewModel (MVVM). This suggested best practice is ideal for creating software that is easy to test and maintain.

# SERVICES AND SILVERLIGHT

In previous chapters, you saw how to use various Web Service technologies to get data into Windows Forms applications, and we will continue to use these concepts with regard to Silverlight. For the most part, this chapter is a review of what you already learned in the previous service chapters, but it points out the differences between calling these services in Silverlight compared to any other type of application.