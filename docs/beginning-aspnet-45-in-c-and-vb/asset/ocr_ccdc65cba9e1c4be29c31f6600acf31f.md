By clicking the link in the message, you are taken to the My Profile page so you can set or change your preferred genres. Unauthorized users are asked to log in or sign up for an account before they can access the Profile page.

![](bbox=[0.15, 0.2, 0.9, 0.48])

FIGURE 17-8

![](bbox=[0.15, 0.53, 0.9, 0.71])

FIGURE 17-9

# How It Works

The code in the Code Behind executes a LINQ to Entities query that retrieves all the reviews that belong to the user's favorite genres. For anonymous users, the list of favorite genres will be empty so they always get to see the message about setting their preferences in the Profile page. To avoid an unnecessary call to the database, the query is executed only when the user has selected at least one preferred genre by checking the Count property of the FavoriteGenres list.