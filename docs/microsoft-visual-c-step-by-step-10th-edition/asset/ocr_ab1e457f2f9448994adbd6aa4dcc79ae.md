consistency if you have to repeatedly set the same properties and values as you add or change controls. The more times you have to do the same thing, the greater the chances are you will get it wrong at least once!

With UWP apps, you can define reusable styles. You can implement them as app-wide resources by creating a resource dictionary to make them available to all controls in all pages in app. You can also define local resources that apply to only a single page in the XAML markup for that page.

In the following exercise, you'll define some simple styles for the Customers app and apply these styles to the controls on the Customers form.

# To define styles for the Customers form

+   1. In Solution Explorer, right-click the **Customers** project, point to **Add**, and then select **New Item**.

+   2. In the left pane of the Add New Item – Customers dialog, select **Visual C#**. In the middle pane, select **Resource Dictionary**. In the name box, select **AppStyles.xaml**, and select **Add**.

![](bbox=[0.158, 0.506, 0.871, 0.888])