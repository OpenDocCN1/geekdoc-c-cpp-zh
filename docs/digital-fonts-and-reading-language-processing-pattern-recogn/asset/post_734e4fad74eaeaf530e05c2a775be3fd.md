
Although the software which renders text to screen is critical, the font itself may also contain software to help it render well. The software in the fonts is referred to as 'hints'. These hints supplement the local text rendering software. When they are used they influence the reproduction of the font's image on screen by temporarily altering the outlines of glyphs and sometimes also the spacing of the font. Hints can be considered a form of font optimization in part because they can be used to improve the appearance of a font on screens but also because for a given use they are effectively altering the shapes of glyphs for that use.

Hinting is powerful but it works better when the shapes found in fonts have been altered to get optimal results. For example in early versions of TTFAutohint if the height of overshoots and undershoots was made consistent fewer errors in rendering would result. In conventional type design this would not normally be done because it conflicts with the need for optical rather than geometric regularity in the font's design.

![](img/ec32f1c4c71e3d11e7f70f2697253828_160_0.png)

Figure 19: Glyphs 'o' and 'r' showing the height of overshoot from the author's font typeface Meriwether. Image taken from Fontlab Studio 5.

Optically based overshoots vary in height based on the degree to which a shape is pointed or sharp rather than flat. The sharper the shape the more it should overshoot in order to appear to be visually even (Figure 19).

Many of the characteristics that help optimize a font for low resolution screens are held in common with optimizing a font for use at small optical sizes: wider spacing, lower contrast, heavier details and heavier weight. As screen resolution increases type designers have greater freedom in choosing forms and spacing. Historically fonts that have been made specifically for screens will choose a horizontal or vertical d shape rather than diagonal when this is possible.

As of the time of writing screen resolutions that have paper-like detail at typical reading distances have been released for smart phones, laptops and desktops. The iPhone 5 for instance has a pixel density of 325+ pixels per inch or 'ppi'. One of the highest densities known to this author at this time is an astonishing 2098 ppi almost 6.5 times higher.

In the same way that distance and the optical size that results from it can sometimes effectively make differences in printing technology less relevant, differences in rendering software are becoming similarly less perceptible as screen resolutions rise. Better screen resolution means less optimization is necessary for the new high resolution screens as a form of media.

Fonts that were made for low and medium resolution screen use can sometimes look out of place in very high resolution environments. They can be optimized to perform better in high resolution environments by adapting their shapes for larger optical sizes. What is the practical impact?

Microsoft implemented a font family for Windows 8 called Sitka. Sitka comes in six optical versions for each style in the family. Users can select optical sizes for themselves. However the Windows OS also has the novel capability of automatically choosing an optical version of Sitka for the user.

Nick Sherman has taken this idea further by proposing a new font format which instead of presenting or switching automatically between a handful of static instances could instead be made to continuously adapt to conditions like a responsive web site. This kind of font format would in theory make a very broad range of continuous adaptive optimization for screen and other media possible.

ᵈ A good example of this is the lower bowl of the two-story 'g' which John Berry mentions on page 9 of 'Now Read This' a booklet made in 2004 to promote fonts made for the then new Clear Type technology in Windows XP.
ᶜ http://www.androidauthority.com/worlds-highest-ppi-display-2098ppi-oled-display-sony-254182/
ᶠ http://alistapart.com/blog/post/variable-fonts-for-responsive-design

## 1.5 Formal characteristics of the font

There are a large number of observable formal characteristics or design variables found in font designs. When a type is optimized it is these characteristics that will be adjusted.

The more ubiquitous the characteristics within the design the greater its value is likely to be. Weight, contrast, width, slant, and spacing are all examples of characteristics found across an entire font. A font with high contrast or a strong slant is much more likely to need adjustment for media than a design with low or medium slant or contrast.§ The adjustment needed is likely to be a reduction in contrast or slant. Very thin or heavy fonts are more likely to need adjusting than medium weights. Similarly middle widths are less likely to need optimizing than wide or narrow ones.

Some formal characteristics are tied to parts of glyphs. These parts may not occur in every glyph but are instead scattered across the glyphs found in the font. Examples include stems, joints, bowls, and terminals. The frequency that a characteristic has in the script being designed matters a great deal. For example in the Latin script stems are fairly common. However in Cyrillic they dominate. In Greek stems are relatively uncommon and round or bowl shapes dominate. Some scripts such as Chinese and Devanagari have a high proportion of glyphs with a high stroke density and therefore have a large number of joins. Any attempt at optimization should take these script-specific tendencies into account.

Some characteristics are only present in sub-sections of the typeface. Their importance to an optimization process can depend on how the font being optimized will be used. For example, because the lower case tends to predominate in most but not all uses of type the characteristic of this group tends to be quite important to the optimization process. However an all caps use would negate their importance altogether.

§ Distortion applied to low contrast glyphs is less likely to be noticed than when it is applied to high contrast ones. Stronger slants are more likely to render poorly on low resolution screens.

## 1.6 Angle of view

The perspective of the reader should also be considered. A sign for drivers painted on to the surface of a road is an example of optimizing for this factor. In this case the letters are stretched vertically to make them easier to read for drivers while approaching the sign which is printed on the road. See Figures 20 and 21.

![](img/ec32f1c4c71e3d11e7f70f2697253828_163_0.png)

Figure 20: ‘Stop’ sign for drivers. Note the very thick top stroke on the T.

![](img/ec32f1c4c71e3d11e7f70f2697253828_163_1.png)

Figure 21: A similar sign for drivers on a street in Hong Kong.

A street sign that needs to be visible from several angles can benefit from the use of large counters and wider than normal letters. People viewing the sign from a position directly in front of the sign will be able to easily tolerate somewhat wider letters while people who see it from an angle on the left or right sides will benefit from the resistance that wider letters have to compression. Spacing the letters more widely will also help. See Figure 22.

![](img/ec32f1c4c71e3d11e7f70f2697253828_164_0.png)

Figure 22: This is a mock up of an imaginary street sign. A compressed style is used on top; a regular style is used in the middle and a wide style is used on the bottom. The signs have been rotated and given perspective. This set of examples show that compressed letterforms have greater problems of legibility than wide ones as the viewing angle moves increasingly away from centered view. The sign uses the type family Univers.

## 1.7 The reader

When thinking about optimizing for media it is necessary to also think about who the reader might be. It is a mistake for instance to simply assume a single kind of reader who is an adult, and an expert reader and who has perfect vision. Getting some insight into the readership a font is intended for can help you know how to optimize your font. Reading ability can vary for reasons of age, education, interest, and so on. For example we now know that a young reader will benefit from wider than normal word spaces (Pelli and Tillman, 2008). Readers with lower or reduced acuity including older readers will benefit from texts set at larger sizes.

## 1.8 Conclusion

Type is most effectively designed for media when a range of additional information is available. Relatively complete and precise information makes it possible to ground design choices in actual reading circumstances and in the needs of the readers.

## References

Pelli, D. G. and Tillman, K. A. (2008). The uncrowded window of object recognition. Nature Neuroscience, 11(10), pp. 1129-35.
