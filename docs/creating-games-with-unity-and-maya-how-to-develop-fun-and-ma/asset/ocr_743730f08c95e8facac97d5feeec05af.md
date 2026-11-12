# # Nature of Effective Textures

Not all textures are created equal. Some textures (image files) are simply easier to envision in a 3D and texture space. Further, and importantly, some textures draw faster, which in game design is a critical consideration.

# ## Be Square

When we were working on the UV layouts, we were working in the top-right quadrant of the UV texture space. Notice that this quadrant is square. If any textures are imported into a material in Maya, it will still show up square within this space. Because of this, it is generally easier to visualize textures by working with square images. Although materials can be deformed (squash them for instance), we went through great effort to create perfectly squared checks when doing the UV layout. This means that we are assuming the texture is not deformed and the results will be much more predictable.

It is important to notice, however, that texture within Maya (or within Unity) do not have to be square. And there may be times when an oblong texture makes the most sense (a long wall for example); however, Maya will still show it as a square image within the UV Texture Editor. So in most cases it just makes the creation process easier for beginners if they see the texture undistorted.

# ## Power of Two

Video cards draw certain assets quicker than other. Part of this has to do with how computer hardware is able to package information. Start with 1 and multiply it by 2 and in turn multiply each result by 2 and a sequence of numbers will emerge like this: 1, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024, 2048, 4096, and so on. These values are referred to as **power of two (POT)**. Textures work most efficiently if their pixel measurements are one of these packaged values. So if we are working with square textures, think 256×256, 512×512, 1024×1024, 2048×2048, or even 4096×4096.

There was a time not long ago when video cards could not display textures that were not a power of two texture. Most video cards today have some strategy to deal with this; however, this almost always includes some sort of resampling the texture into a power of two texture. This means valuable horsepower is being wasted converting a 300×300 texture down to a 256×256. This waste of processing power usually results in lower frame rates and slower game play.

Maya will happily take any size texture thrown at it with nary a complaint, which can lead to a false sense of security. Additionally, new to Unity 3, Unity will take non-power-of-two textures without griping, either—in fact it won't even alert you (unless you look in the Inspector for each texture) that it's taken in non-power-of-two textures and what it's doing