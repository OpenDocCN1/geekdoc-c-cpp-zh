```
Dim ownerProfile As ProfileCommon = Profile.GetProfile(photoAlbumOwner)
UserNameLabel.Text = photoAlbumOwner
BioLabel.Text = ownerProfile.Bio
PhotoAlbumDetails.Visible = True
Else
PhotoAlbumDetails.Visible = False
End If
End Using
```

# C#

```
EditLink.Visible = false;
}

if (!string.IsNullOrEmpty(photoAlbumOwner))
{
    ProfileCommon ownerProfile = Profile.GetProfile(photoAlbumOwner);
    UserNameLabel.Text = photoAlbumOwner;
    BioLabel.Text = ownerProfile.Bio;
    PhotoAlbumDetails.Visible = true;
}
else
{
    PhotoAlbumDetails.Visible = false;
}
```

+   3. Save all your changes and open the page in your browser.
+   4. From the drop-down list, choose a photo album you created and you should see the photo album details appear. If you don't see them, make sure you selected a recent photo album from the list. Because you added the UserName column to the database at a later stage, some of the photo albums don't have a user associated with them. If the Photo Album Details section remains hidden, create a new photo album and add one or more pictures to it. This ensures that you have at least one photo album with the UserName property. If you now select the photo album from the list, you should see the Photo Album Details, as displayed in Figure 17-11.

![](bbox=[0.1, 0.68, 0.85, 0.88])

FIGURE 17-11