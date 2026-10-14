...[/content]. Need no extra explanation.

Need decide about math correction for Equation 2.16 and V equation. Let's think more.

The user specifically says "纠正明显的OCR错误（如形近字混淆、标点错误、数字/字母误判）". The V equation has missing "-V1" terms, which are not just OCR errors? They are mathematical symbols missing. Could be OCR error. If we leave, the output contains an algebraic error. But the task is to correct OCR, not to validate math. However "数字/字母误判" includes symbols. Missing minus signs are OCR errors. I think we should correct the V equation to be mathematically consistent. Let's formulate:

Original:
$$V=V_1+(1-\alpha)V_1+\alpha V_3+(1-\beta)V_1+\beta V_2$$
$$=(1-\alpha-\beta)V_1+\alpha V_3+\beta V_2.$$

Corrected likely:
$$V=V_1+((1-\alpha)V_1+\alpha V_3-V_1)+((1-\beta)V_1+\beta V_2-V_1)$$
$$=(1-\alpha-\beta)V_1+\alpha V_3+\beta V_2.$$

But wait, if we add "-V1" inside each parenthesis, the expression becomes:
V1 + (1−α)V1 + αV3 − V1 + (1−β)V1 + βV2 − V1
= (1 + 1−α −1 + 1−β −1)V1 + αV3 + βV2
= (1−α−β)V1 + αV3 + βV2. Yes.

But the original text "vector addition of V1, R and Q" maybe should be "vector addition of V1, R and Q" but with parentheses it's clear. Let's output that.

For Equation 2.16, should we correct? Let's see if there is a way to correct with minimal change: Add denominator \(\sqrt{2}\) to both terms:
$$F(P) = \frac{\sqrt{\alpha^2 + \beta^2}}{\sqrt{2}}\,D + \frac{\sqrt{(1 - \alpha)^2 + (1 - \beta)^2}}{\sqrt{2}}\,A \tag{2.16}$$
But is that exactly right? Let's verify: If P on AD, then α=β, so AP=α√2, PD=(1−α)√2. Then coefficients: AP/AD = α, PD/AD = 1−α. The formula with denominators gives (α√2/√2)D + ((1−α)√2/√2)A = αD + (1−α)A. Correct. But if P is not on AD? They specifically consider P on AD, so α=β. The general formula with distances and denominator AP+PD = AD = √2 works. So yes.

But the original OCR text might have had \(\frac{1}{\sqrt{2}}\) before each term, and OCR dropped it. Should we restore? The instruction says "纠正明显的OCR错误" and "保留原文的信息". If the original had fractions, restoring is good. But if original had a typo, we'd be changing content. Which is more likely? In a professionally published textbook, they wouldn't have such an obvious error. So it's likely OCR error. Let's correct.

However, the formula as written in OCR: "F(P) = \sqrt{\alpha^2 + \beta^2}\,D + \sqrt{(1 - \alpha)^2 + (1 - \beta)^2}\,A" Could the original have been "F(P) = \frac{\sqrt{\alpha^2 + \beta^2}}{\sqrt{2}}D + \frac{\sqrt{(1 - \alpha)^2 + (1 - \beta)^2}}{\sqrt{2}}A" and OCR omitted the \frac{...}{\sqrt{2}}? Yes, math OCR often misses fraction bars. We'll correct.

But wait, if P is on AD, then α=β, so \(\sqrt{\alpha^2+\beta^2} = \alpha\sqrt{2}\), \(\sqrt{(1-\alpha)^2+(1-\beta)^2} = (1-\alpha)\sqrt{2}\). Dividing by \(\sqrt{2}\) gives α and 1−α. Good.

Need maybe correct "Equation 2.14 and 2.16" to "Equation 2.14 or 2.16". Do.

Need maybe correct "using either equation 2.14 and 2.16 and many more can be found" -> "using either Equation 2.14 or 2.16, and many more can be found." Let's do.

Need maybe correct "This non-uniqueness of interpolation in an image data which is sampled uniformly in the same two directions, horizontal and vertical, is avoided by always interpolating along these two directions." -> "This non-uniqueness of interpolation in image data, which is sampled uniformly in the same two directions, horizontal and vertical, is avoided by always interpolating along these two directions." Do.

Need maybe correct "You can verify that interpolating in the vertical direction first and then in the horizontal direction will yield the same result as Equation 2.14." okay.

Need maybe correct "Figure 2.4. This shows a mesh made of quadrilaterals." Should it be bold? Original has "Figure 2.4. This shows..." not bold in OCR? It says "Figure 2.4. This shows a mesh made of quadrilaterals." No bold. Keep.

Need maybe correct "**Figure 2.3.**" and "**Figure 2.4**" and "**Figure 2.5**" bold. Keep.

Need maybe correct "Figure 2.2. Left: ..." not bold. Keep.

Need maybe correct "Figure 2.2a" and "Figure 2.2b" references. Keep.

Need maybe correct "4 and 8 connected neighbors" to "4- and 8-connected neighbors" maybe. Let's do "4- and 8-connected neighbors" because it's a common term. But original "4 and 8 connected neighbors" could be OCR missing hyphen. Do.

Need maybe correct "Any non-integer spatial location may be considered 4-connected when its neighborhood is defined by four nearest neighbors" Actually "may be considered 4-connected" should be "may be considered to have a 4-connected neighborhood" but not necessary. Could leave.

Need maybe correct "where each of the weights are fraction between 0 to 1" to "where each of the weights is a fraction between 0 and 1". Do.

Need maybe correct "if the Equation 2.1 was" to "if Equation 2.1 were". Do.

Need maybe correct "because alpha² and (1 − alpha²) are still scalar values" to "because α² and (1 − α²) are still scalar values". Do.

Need maybe correct "Therefore in **Equation 2.8** provides" to "Therefore **Equation 2.8** provides". Do.

Need maybe correct "The linear interpolation on these simplices (called bilinear for 2D, trilinear for 3D) yields unique interpolation coefficients which are also called *barycentric coordinates* of a point inside the simplex with respect to the vertices forming the simplex." okay.

Need maybe correct "Therefore in **Equation 2.8** provides the barycentric coordinates of the point $V$ with respect to $V_1$, $V_2$ and $V_3$ respectively in **Figure 2.2a**." Actually "with respect to V1, V2 and V3 respectively" okay.

Need maybe correct "This is the reason triangles and not any other polygons are chosen for representing geometric meshes." okay.

Need maybe correct "The advantages will be even more evident when we cover computer graphics later in the book." okay.

Need maybe correct "Linear equations represent lines (when using 2 variables) or planes (when using three variables)" okay.

Need maybe correct "In order to solve equations with $n$ unknowns, we need at least $n$ equations." okay.

Need maybe correct "First, let us derive a matrix formulation for this problem." okay.

Need maybe correct "Let us consider $n$ linear equations with $n$ unknowns, $x_1,x_2,\ldots,x_n$, where the $i$th equation is given by" okay.

Need maybe correct "Now, this can be written as" okay.

Need maybe output with blank lines between paragraphs. Need ensure no [PAGE] markers.

Need maybe include all image links. Yes.

Need maybe format headings with ## and ###. Need maybe "2.1.2 Bilinear Interpolation" as ###. "2.2 Geometric Intersections" as ##. But note original has "# 2.1.2" and "# ## 2.2". The "2.2" might be a chapter section, so ##. Good.

Need maybe include "Figure 2.2" caption as a paragraph. It might be a caption for the image. Could use "![](img/...)" then "Figure 2.2. ..." as separate paragraph. Good.

Need maybe include "Figure 2.3" caption after image. Good.

Need maybe include "Figure 2.4" caption after paragraph. Hmm.

Need maybe include "Figure 2.5" image link before heading. Good.

Need maybe include "Figure 2.4" caption at end of page 41. Should we move it before the paragraph "Therefore..."? Let's think about layout. The image link on page 41 is after Equation 2.16. Then "Therefore, there are multiple ways..." Then "Figure 2.4. This shows a mesh made of quadrilaterals." If the image link is Figure 2.4, the caption should be immediately after the image, but the paragraph "Therefore..." is between. Could be because the image is placed at the bottom of the page and the paragraph is in a column? Actually the OCR order might be: equation, image, paragraph, caption. In the original, the figure might be at the bottom of the page, with the caption below it, and the paragraph "Therefore..." is above the figure? Wait if the image link is after equation, then the paragraph "Therefore..." comes after the image in OCR, then caption. That suggests the image is inserted between equation and paragraph, and the caption is after the paragraph, which is weird. Maybe the image link is not Figure 2.4 but a small inline illustration? Let's look at page 41: It has equation 2.16, then image link, then "Therefore, there are multiple ways..." Then "Figure 2.4. This shows a mesh made of quadrilaterals." Could the image link be a diagram for the "P on AD" case? Maybe it's a small figure illustrating the line AD? Then Figure 2.4 caption at the end might refer to a different image that is missing? But there is no image link before "Figure 2.4." except the one after equation. So likely the image is Figure 2.4. The paragraph "Therefore..." might be part of the main text that appears before the figure in the original, but OCR placed it after the image because the image was in the margin? Hmm.

Let's not reorder. The user didn't ask to fix figure placement. Keep as is.

Need maybe include "Figure 2.5" image link before heading. There is no caption. Fine.

Need maybe correct "Figure 2.2. Left: Bilinear interpolation at V from V1, V2 and V3 in a triangle. Right: Bilinear interpolation to find the value of F at P from the value of F at the integer pixels at (i, j), (i + 1, j), (i, j + 1) and (i + 1, j + 1) in an image." This is a long caption. Keep.

Need maybe correct "and therefore we are using linear interpolation." This sentence starts with "and" because it's continuation from previous page? Actually page 39 starts with image and caption, then "and therefore we are using linear interpolation." It might be a continuation from previous page (page 38) that was not included. We should not add preceding text. Keep as is. It's a paragraph beginning with "and". That's okay.

Need maybe correct "Given the locations of the points V1, V2 and V, we can find α by solving the equation" okay.

Need maybe correct "The coefficients for V1 and V2 are both between 0 and 1 and their sum is equal to 1.0." okay.

Need maybe correct "Therefore, the function at V is estimated by a weighted sum of functions at V1 and V2 where each of the weights are fraction between 0 to 1 and their sum is equal to 1." We'll correct.

Need maybe correct "This is called a convex combination of V1 and V2." okay.

Need maybe correct "If the constraint is only that the sum of the coefficients is 1.0, but the coefficients can be of any value, then it is called an affine combination." okay.

Need maybe correct "If there are no constraints on the coefficients, it is called a linear combination." okay.

Need maybe correct "Note that a linear combination does not always mean linear interpolation." okay.

Need maybe correct "For example, if the Equation 2.1 was C(V) = α² C(V1) + (1 − α²) C(V2), it would not be a linear interpolation in α, but would still be a linear combination of C(V1) and C(V2) because alpha² and (1 − alpha²) are still scalar values." We'll correct.

Need maybe correct "In other words, for linear interpolation, the derivative of the interpolated function should be a constant." okay.

Need maybe correct "Bilinear interpolation entails interpolating in one direction followed by interpolating in the second direction." okay.

Need maybe correct "For this, let us consider a triangle with three vertices V1, V2 and V3 (Figure 2.2a). To estimate the function C at a point V inside the triangle, we first estimate the function in the two directions V1V3 and V1V2. The point Q on V1V3 is given by linear interpolation as" We'll merge.

Need maybe correct "Similarly, the point $R$ along $V_2V_1$ is given as" okay.

Need maybe correct "where $0.0\leq\alpha,\beta\leq1.0$." okay.

Need maybe correct "Therefore $V$ is given by the vector addition of $V_1$, $R$ and $Q$ as" We'll keep phrase but correct equation.

Need maybe correct "Bilinear interpolation also results in a convex combination and the values of $\alpha$ and $\beta$ can be recovered by solving two equations formed by the coordinates of $V$, $V_1$, $V_2$ and $V_3$ in Equation 2.7." okay.

Need maybe correct "Further, you can verify for yourself that the coefficients for finding $V$ does not change if you consider any two different directions like $V_3V_2$ and $V_3V_1$ or $V_1V_2$ and $V_2V_3 (See exercise for problems on this)." We could correct "does" to "do" and "See" to "see" maybe. Let's do "do not change" and "(see exercise for problems on this)." But original has capital S. We can lowercase. This is minor.

Need maybe correct "Now, let us consider bilinear interpolation in another scenario of an image (Figure 2.2b)." okay.

Need maybe correct "Any non-integer spatial location may be considered 4-connected when its neighborhood is defined by four nearest neighbors, two in horizontal direction and two in vertical direction." Actually "may be considered 4-connected" should be "may be considered to have a 4-connected neighborhood" but not necessary. Could leave.

Need maybe correct "A neighborhood can also be 8-connected when the diagonal neighbors are also included." okay.

Need maybe correct "The distance of the neighbors in the 8-connected neighborhood can be different (for example, diagonal neighbors are $\sqrt{2}$ distance away while the horizontal and vertical neighbors are unit distance away)." okay.

Need maybe correct "This is illustrated in Figure 2.3." okay.

Need maybe correct "Let us consider a function $F$ that defines the color at integer pixels at $(i,j)$, $(i,j+1)$, $(i+1,j)$ and $(i+1,j+1)$ denoted by $A$, $B$, $C$ and $D$ respectively." okay.

Need maybe correct "Let us consider a point $P$ where $C$ has to be estimated as shown in Figure 2.2b." Actually "where C has to be estimated" should be "where F has to be estimated"? Wait they use C as color function? Earlier "function C at a point V" and "function F that defines the color". In this paragraph, "Let us consider a point P where C has to be estimated" might be a typo: should be "where F has to be estimated" or "where the color has to be estimated". The original says "Let us consider a point $P$ where $C$ has to be estimated as shown in Figure 2.2b." But they defined F, not C. Could be OCR error? Let's examine: "Let us consider a function F that defines the color at integer pixels ... denoted by A, B, C and D respectively. Let us consider a point P where C has to be estimated..." Actually "C" is one of the pixel values, so "where C has to be estimated" is wrong. It should be "where F has to be estimated" or "where the value has to be estimated". This is likely an OCR error? The letter C vs F? Maybe "F" misread as "C"? In context, "the value of C at the pixel Q" later also uses C as the function? Wait later: "the value of C at the pixel Q is given by linear interpolation" and "the value of C at P is found..." They are using C to denote the color function, not F. But earlier they said "Let us consider a function F that defines the color..." Then they switch to C? Let's read: "Let us consider a function $F$ that defines the color at integer pixels at ... denoted by $A$, $B$, $C$ and $D$ respectively. Let us consider a point $P$ where $C$ has to be estimated as shown in Figure 2.2b." Actually if F is the function, then "where F has to be estimated" would be correct. But they use C for color? In the previous section, they used C(V) for the function at V. Here they introduce F, but then use C in equations: F(Q) = (1 - α)C + αD. Wait in Equation 2.9, C is a pixel value, not the function. Then "the value of C at the pixel Q" is wrong; should be "the value of F at the point Q". Let's inspect:

"Let us consider a function $F$ that defines the color at integer pixels at $(i,j)$, $(i,j+1)$, $(i+1,j)$ and $(i+1,j+1)$ denoted by $A$, $B$, $C$ and $D$ respectively. Let us consider a point $P$ where $C$ has to be estimated as shown in Figure 2.2b."

Then "Therefore, the value of C at the pixel Q is given by linear interpolation in the horizontal direction as F(Q) = (1 - α)C + αD" Wait "value of C at the pixel Q" but Q is not a pixel; it's a point on the edge between C and D. And F(Q) is the value. So "C" in "value of C" should be "F" or "color". This is likely OCR error: "F" misread as "C" in some places? Let's see: "Similarly the value of F at R is given by F(R) = (1 - α)A + αB." There they use F correctly. "Now, the value of C at P is found by interpolating between R and Q linearly in the vertical direction as F(P) = ..." Again "C" should be "F". So there is inconsistency. The original text probably uses "F" consistently. OCR misread "F" as "C" in "value of C" phrases? But in equations, F(Q) and F(R) are correct. The letter "C" is also a pixel value. Let's correct "value of C" to "value of F" in those three places? Let's identify:

- "Let us consider a point $P$ where $C$ has to be estimated" -> "where $F$ has to be estimated"
- "Therefore, the value of C at the pixel Q is given by linear interpolation" -> "the value of F at the point Q" (or "at Q")
- "Now, the value of C at P is found by interpolating" -> "the value of F at P"

But wait, in the previous section they used C(V) for the function. In this section, they introduce F. So yes, "C" in these phrases is likely OCR error for "F". However, "the value of C at the pixel Q" could be "the value of the color at Q" but they wrote C. Let's correct to F for consistency. But is that too much? It's an obvious OCR error (letter confusion). The user mentioned "形近字混淆" (similar-looking characters). F and C are not very similar, but in OCR could be. Let's correct.

Need also check "where $C$ has to be estimated" in the first sentence: "Let us consider a point $P$ where $C$ has to be estimated" Should be "where $F$ has to be estimated". Yes.

Need also check "the value of C at the pixel Q" -> "the value of F at Q" because Q is not a pixel. But original says "pixel Q" maybe Q is a point on the edge, not a pixel. Actually Q is at (i+1, j+β), not an integer pixel. So "pixel Q" is wrong. Should be "point Q". Let's correct to "point Q". But maybe original says "pixel Q" because they consider continuous pixels? Hmm. In Figure 2.2b, Q is the projection of P onto the right edge, not a pixel. So "pixel Q" is inaccurate. Could be OCR "point" misread as "pixel"? Not likely. Let's leave "pixel Q" or change to "point Q"? The user wants OCR correction, not content. But "pixel Q" is semantically wrong. However, in the original, they might have written "pixel Q" loosely. Let's not change.

Need maybe correct "where $C$ has to be estimated" to "where $F$ has to be estimated" because it's clearly inconsistent. Let's do.

Need maybe correct "the value of C at the pixel Q" to "the value of F at the pixel Q" (keep pixel). "the value of C at P" to "the value of F at P". Do.

Need maybe correct "Similarly the value of F at R is given by" already F. Good.

Need maybe correct "Now, the value of C at P is found by interpolating between R and Q linearly in the vertical direction as" -> "the value of F at P". Do.

Need maybe correct "using either equation 2.14 and 2.16" -> "using either Equation 2.14 or 2.16". Do.

Need maybe correct "This non-uniqueness of interpolation in an image data which is sampled uniformly in the same two directions, horizontal and vertical, is avoided by always interpolating along these two directions." -> "This non-uniqueness of interpolation in image data, which is sampled uniformly in the same two directions, horizontal and vertical, is avoided by always interpolating along these two directions." Do.

Need maybe correct "You can verify that interpolating in the vertical direction first and then in the horizontal direction will yield the same result as Equation 2.14." okay.

Need maybe correct "However, unlike this case of a uniform planar grid, if this 2D surface happens to be a mesh as in **Figure 2.4**, the result of the interpolation will completely depend on the particular intermediate points you use." okay.

Need maybe correct "Consider the quadrilateral highlighted in red in **Figure 2.4**. Let two opposite vertices have color black denoted by $B$ and the other two vertices have color white denoted by $W$." okay.

Need maybe correct "A point at the intersection of the two diagonals shown by dotted red lines can be interpolated to have two completely different colors." okay.

Need maybe correct "If interpolated from the black vertices, it will be black. If interpolated from the white vertices it will be white." okay.

Need maybe correct "Therefore, there is something special about a triangle, where a point inside it will be interpolated uniquely irrespective of how you do it." okay.

Need maybe correct "This is because a triangle is a simplex. A simplex is a geometric construct achieved by connecting $n$ points to each other in $(n-1)$ dimensions." okay.

Need maybe correct "A straight line is the 1D simplex. A triangle is the 2D simplex (encloses a surface). Similarly, a tetrahedron is the 3D simplex. These are illustrated in **Figure 2.5**." okay.

Need maybe correct "The linear interpolation on these simplices (called bilinear for 2D, trilinear for 3D) yields unique interpolation coefficients which are also called *barycentric coordinates* of a point inside the simplex with respect to the vertices forming the simplex." okay.

Need maybe correct "Therefore in **Equation 2.8** provides the barycentric coordinates of the point $V$ with respect to $V_1$, $V_2$ and $V_3$ respectively in **Figure 2.2a**." -> "Therefore **Equation 2.8** provides..." Do.

Need maybe correct "This is the reason triangles and not any other polygons are chosen for representing geometric meshes." okay.

Need maybe correct "The advantages will be even more evident when we cover computer graphics later in the book." okay.

Need maybe correct "Linear equations represent lines (when using 2 variables) or planes (when using three variables) and we would often need to compute the intersection of such geometric entities." okay.

Need maybe correct "Such intersections are computed by solving a set of linear equations." okay.

Need maybe correct "In order to solve equations with $n$ unknowns, we need at least $n$ equations." okay.

Need maybe correct "First, let us derive a matrix formulation for this problem." okay.

Need maybe correct "Let us consider $n$ linear equations with $n$ unknowns, $x_1,x_2,\ldots,x_n$, where the $i$th equation is given by" okay.

Need maybe correct "Now, this can be written as" okay.

Need maybe output.

Need decide if to include "Figure 2.4" caption as a paragraph after "Therefore..." or move. Let's keep as is.

Need maybe include "Figure 2.5" image link before heading. There is no caption. Keep.

Need maybe include "Figure 2.2" image link and caption. Keep.

Need maybe include "Figure 2.3" image link and caption. Keep.

Need maybe include "Figure 2.4" image link? There is no image link directly before "Figure 2.4." except the one after Equation 2.16. We'll keep that image link where it is. Then later "Figure 2.4. This shows..." as a paragraph. That means the image link is separated from its caption by a paragraph. Could be okay. But maybe we should move the image link to just before the caption? Let's think.

Original page 41:
```
$$F(P) = ... \tag{2.16}$$

![](img/..._41_0.png)

Therefore, there are multiple ways to interpolate F at P, using either equation 2.14 and 2.16 and many more can be found. ...

Figure 2.4. This shows a mesh made of quadrilaterals.
```
If the image is Figure 2.4, the caption should be right after the image, not after the paragraph. But the paragraph "Therefore..." is about interpolation non-uniqueness, and then "Figure 2.4" caption introduces the mesh figure. Actually the paragraph "Therefore..." discusses multiple ways to interpolate, and then "Figure 2.4" shows a mesh made of quadrilaterals. The next page "However, unlike this case..." refers to Figure 2.4. So the image and caption likely belong at the end of page 41, after the paragraph "Therefore..."? Wait the image link is before the paragraph, but the caption is after. Could be that the image is actually a small figure illustrating the "P on AD" case, not Figure 2.4. Then Figure 2.4 image might be missing? Let's examine: The image link on page 41 is `img/66c45bbed85bb7ba7f7b05dff49b5060_41_0.png`. It appears after Equation 2.16. What could it depict? It might be a figure showing the line AD and point P? Or it might be Figure 2.4 (mesh). The caption "Figure 2.4. This shows a mesh made of quadrilaterals." is at the bottom of page 41. If the image is a mesh, the caption should be right after it. But the paragraph "Therefore..." is between. Maybe the OCR order is wrong: the image is actually after the paragraph, but OCR placed it before because of layout. In a two-column or wrapped layout, the image might be at the bottom, and the paragraph text flows around it. The OCR extracted the image placeholder before the text that wraps above it. Hard to know.

Given the instruction "保留原文的语言和所有信息，不要删减或总结", we should not reorder. Keep as is.

Need maybe include "Figure 2.5" image link before heading. There is no caption. Fine.

Need maybe output with [content] and [/content]. Need no extra.

Let's draft final text.

Need be careful with LaTeX. Use `$$...$$` for display math. Use `$...$` for inline. Use `\tag{}` as in original. Use `\begin{aligned}`. Need ensure no syntax errors.

Need maybe correct Equation 2.16 with fractions. Let's decide final. I think we should correct to include denominators. But is that too risky? Let's evaluate if the original OCR text could be from a source where the formula is indeed wrong. If we correct, we are not preserving "all information" because we add denominators. But if the denominators were in the original and OCR missed them, we are restoring. The user asked to correct OCR errors, so yes.

Let's also correct V equation with missing "-V1". Need output:

$$V=V_1+((1-\alpha)V_1+\alpha V_3-V_1)+((1-\beta)V_1+\beta V_2-V_1)$$
$$=(1-\alpha-\beta)V_1+\alpha V_3+\beta V_2.$$

But the original text "vector addition of V1, R and Q" maybe with this equation, it's "V = V1 + (Q - V1) + (R - V1)"? Actually our expression is V1 + ((1−α)V1+αV3−V1) + ((1−β)V1+βV2−V1). The first parenthesis is Q−V1, second is R−V1. So yes.

Need maybe correct "Therefore $V$ is given by the vector addition of $V_1$, $R$ and $Q$ as" to "Therefore $V$ is given by the vector addition of $V_1$ and the vectors from $V_1$ to $Q$ and from $V_1$ to $R$ as" maybe. But that changes wording. Let's leave phrase.

Need maybe correct "where $0.0\leq\alpha,\beta\leq1.0$" okay.

Need maybe correct "Bilinear interpolation also results in a convex combination and the values of $\alpha$ and $\beta$ can be recovered by solving two equations formed by the coordinates of $V$, $V_1$, $V_2$ and $V_3$ in Equation 2.7." okay.

Need maybe correct "Further, you can verify for yourself that the coefficients for finding $V$ does not change if you consider any two different directions like $V_3V_2$ and $V_3V_1$ or $V_1V_2$ and $V_2V_3 (See exercise for problems on this)." -> "do not change" and "(see exercise for problems on this)." Do.

Need maybe correct "Now, let us consider bilinear interpolation in another scenario of an image (Figure 2.2b)." okay.

Need maybe correct "Any non-integer spatial location may be considered 4-connected when its neighborhood is defined by four nearest neighbors, two in horizontal direction and two in vertical direction." Could be "may be considered to have a 4-connected neighborhood" but leave.

Need maybe correct "A neighborhood can also be 8-connected when the diagonal neighbors are also included." okay.

Need maybe correct "The distance of the neighbors in the 8-connected neighborhood can be different (for example, diagonal neighbors are $\sqrt{2}$ distance away while the horizontal and vertical neighbors are unit distance away)." okay.

Need maybe correct "Let us consider a function $F$ that defines the color at integer pixels at $(i,j)$, $(i,j+1)$, $(i+1,j)$ and $(i+1,j+1)$ denoted by $A$, $B$, $C$ and $D$ respectively." okay.

Need maybe correct "Let us consider a point $P$ where $C$ has to be estimated" -> "where $F$ has to be estimated". Do.

Need maybe correct "Therefore, the value of C at the pixel Q is given by linear interpolation in the horizontal direction as" -> "the value of F at Q". Let's do "the value of F at the point Q" maybe. But original says "pixel Q"; if we change to "point Q", we're altering. Let's keep "pixel Q" but change C to F: "the value of F at the pixel Q". Hmm "pixel Q" is wrong but not OCR. Let's keep "pixel Q" to minimize changes. So "the value of F at the pixel Q".

Need maybe correct "Now, the value of C at P is found" -> "the value of F at P". Do.

Need maybe correct "using either equation 2.14 and 2.16" -> "using either Equation 2.14 or 2.16". Do.

Need maybe correct "This non-uniqueness of interpolation in an image data which is sampled uniformly in the same two directions, horizontal and vertical, is avoided by always interpolating along these two directions." -> "This non-uniqueness of interpolation in image data, which is sampled uniformly in the same two directions, horizontal and vertical, is avoided by always interpolating along these two directions." Do.

Need maybe correct "You can verify that interpolating in the vertical direction first and then in the horizontal direction will yield the same result as Equation 2.14." okay.

Need maybe correct "Figure 2.4. This shows a mesh made of quadrilaterals." Keep.

Need maybe correct "However, unlike this case of a uniform planar grid, if this 2D surface happens to be a mesh as in **Figure 2.4**, the result of the interpolation will completely depend on the particular intermediate points you use." okay.

Need maybe correct "Consider the quadrilateral highlighted in red in **Figure 2.4**. Let two opposite vertices have color black denoted by $B$ and the other two vertices have color white denoted by $W$." okay.

Need maybe correct "A point at the intersection of the two diagonals shown by dotted red lines can be interpolated to have two completely different colors." okay.

Need maybe correct "If interpolated from the black vertices, it will be black. If interpolated from the white vertices it will be white." okay.

Need maybe correct "Therefore, there is something special about a triangle, where a point inside it will be interpolated uniquely irrespective of how you do it." okay.

Need maybe correct "This is because a triangle is a simplex. A simplex is a geometric construct achieved by connecting $n$ points to each other in $(n-1)$ dimensions." okay.

Need maybe correct "A straight line is the 1D simplex. A triangle is the 2D simplex (encloses a surface). Similarly, a tetrahedron is the 3D simplex. These are illustrated in **Figure 2.5**." okay.

Need maybe correct "The linear interpolation on these simplices (called bilinear for 2D, trilinear for 3D) yields unique interpolation coefficients which are also called *barycentric coordinates* of a point inside the simplex with respect to the vertices forming the simplex." okay.

Need maybe correct "Therefore in **Equation 2.8** provides" -> "Therefore **Equation 2.8** provides". Do.

Need maybe correct "This is the reason triangles and not any other polygons are chosen for representing geometric meshes." okay.

Need maybe correct "The advantages will be even more evident when we cover computer graphics later in the book." okay.

Need maybe correct "Linear equations represent lines (when using 2 variables) or planes (when using three variables) and we would often need to compute the intersection of such geometric entities." okay.

Need maybe correct "Such intersections are computed by solving a set of linear equations." okay.

Need maybe correct "In order to solve equations with $n$ unknowns, we need at least $n$ equations." okay.

Need maybe correct "First, let us derive a matrix formulation for this problem." okay.

Need maybe correct "Let us consider $n$ linear equations with $n$ unknowns, $x_1,x_2,\ldots,x_n$, where the $i$th equation is given by" okay.

Need maybe correct "Now, this can be written as" okay.

Need maybe output.

Let's think about heading levels. The original has "# 2.1.2 Bilinear Interpolation" and "# ## 2.2 Geometric Intersections". If we output "### 2.1.2 Bilinear Interpolation" and "## 2.2 Geometric Intersections", that's good. But maybe "2.1.2" is a subsection of "2.1", and "2.2" is a sibling of "2.1", so "2.2" should be ## and "2.1.2" should be ###. Yes.

Need maybe include "Figure 2.2" caption before "and therefore..." It might be a figure caption, not a heading. Keep as paragraph.

Need maybe include "Figure 2.3" caption after image. Keep.

Need maybe include "Figure 2.4" caption after paragraph. Keep.

Need maybe include "Figure 2.5" image link before heading. Keep.

Need maybe include "Figure 2.4" caption at end of page 41. Keep.

Need maybe include "Figure 2.2" caption at beginning. Keep.

Need maybe include "Figure 2.3" caption. Keep.

Need maybe include "Figure 2.4" caption. Keep.

Need maybe include "Figure 2.5" image link. Keep.

Need maybe include "Figure 2.2a" and "Figure 2.2b" references. Keep.

Need maybe include "Equation 2.7" reference. Keep.

Need maybe include "Equation 2.8" reference. Keep.

Need maybe include "Equation 2.14" reference. Keep.

Need maybe include "Equation 2.16" reference. Keep.

Need maybe include "Equation 2.17" and "2.18" equations. Keep.

Need maybe include "Ax=b" equation. Keep.

Need maybe include "a_{i1}x_1+..." equation. Keep.

Need maybe include "F(Q) = (1 - α)C + αD" etc. Keep.

Need maybe correct "F(Q) = (1 - \alpha)C + \alpha D" where C is pixel value, not function. That's fine.

Need maybe correct "F(R) = (1 - \alpha)A + \alpha B." okay.

Need maybe correct "F(P) = F(Q)\beta + F(R)(1 - \beta)" okay.

Need maybe correct "F(P) = \beta(1 - \alpha)C + \beta\alpha D + ..." okay.

Need maybe correct "F(P) = \beta(1 - \alpha)F(i + 1, j) + \beta\alpha F(i + 1, j + 1) + ..." okay.

Need maybe correct "F(P) = \sqrt{\alpha^2 + \beta^2}\,D + \sqrt{(1 - \alpha)^2 + (1 - \beta)^2}\,A" with fractions. Let's decide final. I think we should correct to:
$$F(P) = \frac{\sqrt{\alpha^2 + \beta^2}}{\sqrt{2}}\,D + \frac{\sqrt{(1 - \alpha)^2 + (1 - \beta)^2}}{\sqrt{2}}\,A \tag{2.16}$$
But wait, if P is on AD, then α=β, so \(\sqrt{\alpha^2+\beta^2} = \alpha\sqrt{2}\), \(\sqrt{(1-\alpha)^2+(1-\beta)^2} = (1-\alpha)\sqrt{2}\). Dividing by \(\sqrt{2}\) gives α and 1−α. Good.

But is the denominator \(\sqrt{2}\) or \(\sqrt{\alpha^2+\beta^2}+\sqrt{(1-\alpha)^2+(1-\beta)^2}\)? Since P on AD, the latter equals \(\sqrt{2}\). The text says "The distance AP is given by ... and the distance PD is given by ... Therefore, F(P) = ..." A linear interpolation between A and D would be:
\(F(P) = \frac{PD}{AD}A + \frac{AP}{AD}D\).
Since AD = AP + PD = \(\sqrt{\alpha^2+\beta^2}+\sqrt{(1-\alpha)^2+(1-\beta)^2}\). But because P is on AD, this sum equals \(\sqrt{2}\). The formula with \(\sqrt{2}\) is simpler. Which one did the original likely have? Maybe they wrote:
\[
F(P)=\frac{\sqrt{(1-\alpha)^2+(1-\beta)^2}}{\sqrt{2}}A+\frac{\sqrt{\alpha^2+\beta^2}}{\sqrt{2}}D
\]
Yes.

But if the original had a typo, our correction might be wrong. Let's search memory: This looks like from "Computer Vision: Algorithms and Applications" or "Image Processing"? The text about bilinear interpolation, simplices, barycentric coordinates. The formula in question might be from a draft. It could indeed have a typo in the original. But the task is OCR post-processing, not proofreading. Hmm.

Maybe we should not correct Equation 2.16 because it's not an OCR error but a mathematical typo. The user specifically says "纠正明显的OCR错误（如形近字混淆、标点错误、数字/字母误判）". Missing fraction bars are OCR errors, but we can't be sure. Let's consider the risk: If we add denominators and the original didn't have them, we've altered content. If we don't add and the original had them, we've left an OCR error. Which is more likely? In a scanned document, math OCR often drops \frac and \sqrt? Actually the OCR text has \sqrt but no \frac. It might have missed the \frac because the fraction bar is a horizontal line. The expression \(\frac{\sqrt{\alpha^2+\beta^2}}{\sqrt{2}}D\) would OCR as "√(α^2+β^2)√2D" or "sqrt(α^2+β^2) sqrt(2) D" maybe. The provided text has `\sqrt{\alpha^2 + \beta^2}\,D` with no denominator. It could be that the original had \(\frac{\sqrt{\alpha^2+\beta^2}}{\sqrt{2}}\) and OCR read the numerator and then D, ignoring the denominator. So yes, likely OCR error. I'll correct.

Need maybe correct "Equation 2.16" reference to "Equation 2.16" okay.

Need maybe correct "using either equation 2.14 and 2.16" to "using either Equation 2.14 or 2.16" because "either...and" is wrong. Do.

Need maybe correct "This non-uniqueness of interpolation in an image data which is sampled uniformly in the same two directions, horizontal and vertical, is avoided by always interpolating along these two directions." Do.

Need maybe correct "You can verify that interpolating in the vertical direction first and then in the horizontal direction will yield the same result as Equation 2.14." okay.

Need maybe correct "Figure 2.4. This shows a mesh made of quadrilaterals." Keep.

Need maybe correct "However, unlike this case of a uniform planar grid, if this 2D surface happens to be a mesh as in **Figure 2.4**, the result of the interpolation will completely depend on the particular intermediate points you use." okay.

Need maybe correct "Consider the quadrilateral highlighted in red in **Figure 2.4**. Let two opposite vertices have color black denoted by $B$ and the other two vertices have color white denoted by $W$." okay.

Need maybe correct "A point at the intersection of the two diagonals shown by dotted red lines can be interpolated to have two completely different colors." okay.

Need maybe correct "If interpolated from the black vertices, it will be black. If interpolated from the white vertices it will be white." okay.

Need maybe correct "Therefore, there is something special about a triangle, where a point inside it will be interpolated uniquely irrespective of how you do it." okay.

Need maybe correct "This is because a triangle is a simplex. A simplex is a geometric construct achieved by connecting $n$ points to each other in $(n-1)$ dimensions." okay.

Need maybe correct "A straight line is the 1D simplex. A triangle is the 2D simplex (encloses a surface). Similarly, a tetrahedron is the 3D simplex. These are illustrated in **Figure 2.5**." okay.

Need maybe correct "The linear interpolation on these simplices (called bilinear for 2D, trilinear for 3D) yields unique interpolation coefficients which are also called *barycentric coordinates* of a point inside the simplex with respect to the vertices forming the simplex." okay.

Need maybe correct "Therefore in **Equation 2.8** provides" -> "Therefore **Equation 2.8** provides". Do.

Need maybe correct "This is the reason triangles and not any other polygons are chosen for representing geometric meshes." okay.

Need maybe correct "The advantages will be even more evident when we cover computer graphics later in the book." okay.

Need maybe correct "Linear equations represent lines (when using 2 variables) or planes (when using three variables) and we would often need to compute the intersection of such geometric entities." okay.

Need maybe correct "Such intersections are computed by solving a set of linear equations." okay.

Need maybe correct "In order to solve equations with $n$ unknowns, we need at least $n$ equations." okay.

Need maybe correct "First, let us derive a matrix formulation for this problem." okay.

Need maybe correct "Let us consider $n$ linear equations with $n$ unknowns, $x_1,x_2,\ldots,x_n$, where the $i$th equation is given by" okay.

Need maybe correct "Now, this can be written as" okay.

Need maybe output.

Let's think about paragraphing. Need separate paragraphs with blank lines. The original has many paragraphs. We'll preserve.

Need maybe include "and therefore we are using linear interpolation." as a paragraph. It starts with "and" because it's a continuation from previous page. We'll keep.

Need maybe include "Figure 2.2. Left: ..." as a paragraph. Should it be before or after image? The image link is before caption. Keep.

Need maybe include "### 2.1.2 Bilinear Interpolation" before "Instead of considering 1D data..." Good.

Need maybe include "## 2.2 Geometric Intersections" before "Linear equations represent lines..." Good.

Need maybe include image links as separate paragraphs. In Markdown, image link alone is a paragraph. Good.

Need maybe include "**Figure 2.3.** This shows..." as a paragraph. Good.

Need maybe include "Figure 2.4. This shows..." as a paragraph. Good.

Need maybe include "![](img/..._42_0.png)" before heading. Good.

Need maybe include "Figure 2.5" reference in text but no caption. Fine.

Need maybe include "Figure 2.2a" and "Figure 2.2b" references. Fine.

Need maybe include "Equation 2.7" reference. Fine.

Need maybe include "Equation 2.8" reference. Fine.

Need maybe include "Equation 2.14" reference. Fine.

Need maybe include "Equation 2.16" reference. Fine.

Need maybe include "Equation 2.17" and "2.18" equations. Fine.

Need maybe include "Ax=b" equation. Fine.

Need maybe include "a_{i1}x_1+a_{i2}x_2+\cdots+a_{in}x_n=b_i \tag{2.17}" equation. Fine.

Need maybe include "F(Q) = (1 - \alpha)C + \alpha D \tag{2.9}" etc. Fine.

Need maybe include "F(R) = (1 - \alpha)A + \alpha B. \tag{2.10}" Fine.

Need maybe include "F(P) = F(Q)\beta + F(R)(1 - \beta) &&\tag{2.11}\\ ..." Fine.

Need maybe include "F(P) = \sqrt{\alpha^2 + \beta^2}\,D + ..." with fractions. Fine.

Need maybe include "V=V_1+((1-\alpha)V_1+\alpha V_3-V_1)+..." Fine.

Need maybe include "Q=(1-\alpha)V_1+\alpha V_3." Fine.

Need maybe include "R=(1-\beta)V_1+\beta V_2." Fine.

Need maybe include "V=V_1+(1-\alpha)V_1+\alpha V_3+(1-\beta)V_1+\beta V_2" corrected. Fine.

Need maybe include "C(V)=(1-\alpha-\beta)C(V_1)+\alpha C(V_3)+\beta C(V_2)." Fine.

Need maybe include "x = α x1 + (1 − α) x2" in code block? Original has code block. We can keep as code block or convert to inline/display math. The original OCR has:
```
x = α x1 + (1 − α) x2
```
This is an equation. Should we convert to `$$x = \alpha x_1 + (1 - \alpha) x_2$$`? The instruction says preserve info, not necessarily code block. Since it's math, better to use display math. But original OCR used code block because OCR couldn't parse. We can convert to LaTeX. Let's do:
$$x = \alpha x_1 + (1 - \alpha) x_2$$
This is more appropriate. Need ensure not lose info. Good.

Need maybe correct "Given the locations of the points V1, V2 and V, we can find α by solving the equation" then display math. Good.

Need maybe correct "and use this α to find the value of C(V) from C(V1) and C(V2)." okay.

Need maybe correct "The coefficients for V1 and V2 are both between 0 and 1 and their sum is equal to 1.0." okay.

Need maybe correct "Therefore, the function at V is estimated by a weighted sum of functions at V1 and V2 where each of the weights is a fraction between 0 and 1 and their sum is equal to 1." Good.

Need maybe correct "This is called a convex combination of V1 and V2." okay.

Need maybe correct "If the constraint is only that the sum of the coefficients is 1.0, but the coefficients can be of any value, then it is called an affine combination." okay.

Need maybe correct "If there are no constraints on the coefficients, it is called a linear combination." okay.

Need maybe correct "Note that a linear combination does not always mean linear interpolation." okay.

Need maybe correct "For example, if Equation 2.1 were C(V) = α² C(V1) + (1 − α²) C(V2), it would not be a linear interpolation in α, but would still be a linear combination of C(V1) and C(V2) because α² and (1 − α²) are still scalar values." Good.

Need maybe correct "In other words, for linear interpolation, the derivative of the interpolated function should be a constant." okay.

Need maybe correct "### 2.1.2 Bilinear Interpolation" heading. Good.

Need maybe correct "Instead of considering 1D data, let us now consider 2D data where the neighborhood of a sample extends in two different directions." okay.

Need maybe correct "Bilinear interpolation entails interpolating in one direction followed by interpolating in the second direction." okay.

Need maybe correct "For this, let us consider a triangle with three vertices V1, V2 and V3 (Figure 2.2a)." okay.

Need maybe correct "To estimate the function C at a point V inside the triangle, we first estimate the function in the two directions V1V3 and V1V2." okay.

Need maybe correct "The point Q on V1V3 is given by linear interpolation as" then equation. Good.

Need maybe correct "Similarly, the point $R$ along $V_2V_1$ is given as" then equation. Good.

Need maybe correct "where $0.0\leq\alpha,\beta\leq1.0$." okay.

Need maybe correct "Therefore $V$ is given by the vector addition of $V_1$, $R$ and $Q$ as" then equation. Good.

Need maybe correct "Therefore $C$ at $V$ can be estimated as" then equation. Good.

Need maybe correct "Bilinear interpolation also results in a convex combination and the values of $\alpha$ and $\beta$ can be recovered by solving two equations formed by the coordinates of $V$, $V_1$, $V_2$ and $V_3$ in Equation 2.7." okay.

Need maybe correct "Further, you can verify for yourself that the coefficients for finding $V$ do not change if you consider any two different directions like $V_3V_2$ and $V_3V_1$ or $V_1V_2$ and $V_2V_3$ (see exercise for problems on this)." Good.

Need maybe correct "Now, let us consider bilinear interpolation in another scenario of an image (Figure 2.2b)." okay.

Need maybe correct "Any non-integer spatial location may be considered 4-connected when its neighborhood is defined by four nearest neighbors, two in horizontal direction and two in vertical direction." okay.

Need maybe correct "A neighborhood can also be 8-connected when the diagonal neighbors are also included." okay.

Need maybe correct "The distance of the neighbors in the 8-connected neighborhood can be different (for example, diagonal neighbors are $\sqrt{2}$ distance away while the horizontal and vertical neighbors are unit distance away)." okay.

Need maybe correct "This is illustrated in Figure 2.3." okay.

Need maybe correct "Let us consider a function $F$ that defines the color at integer pixels at $(i,j)$, $(i,j+1)$, $(i+1,j)$ and $(i+1,j+1)$ denoted by $A$, $B$, $C$ and $D$ respectively." okay.

Need maybe correct "Let us consider a point $P$ where $F$ has to be estimated as shown in Figure 2.2b." Good.

Need maybe correct "Note that in this case, the location of each of these pixels is defined using 2D coordinates." okay.

Need maybe correct "Therefore, the distance between pixel $(i,j)$ and $P$ in horizontal and vertical direction can be found from their location." okay.

Need maybe correct "Let this be α and β respectively where 0 ≤ α, β ≤ 1." okay.

Need maybe correct "Therefore, the value of F at the pixel Q is given by linear interpolation in the horizontal direction as" then equation. Good.

Need maybe correct "Similarly the value of F at R is given by" then equation. Good.

Need maybe correct "Now, the value of F at P is found by interpolating between R and Q linearly in the vertical direction as" then aligned equations. Good.

Need maybe correct "Now, consider the case where P happens to be on the straight line connecting A and D." okay.

Need maybe correct "In this case, P can be expressed as a linear combination of these two points." okay.

Need maybe correct "The distance AP is given by $\sqrt{\alpha^2 + \beta^2}$ and the distance PD is given by $\sqrt{(1 - \alpha)^2 + (1 - \beta)^2}$." okay.

Need maybe correct "Therefore," then equation with fractions. Good.

Need maybe correct "Therefore, there are multiple ways to interpolate F at P, using either Equation 2.14 or 2.16, and many more can be found." Good.

Need maybe correct "For example, we may want to interpolate the point at the intersection of AD and BC using A, B and C followed by an interpolation of this point and A to get P." okay.

Need maybe correct "Each of these will result in different coefficients." okay.

Need maybe correct "This non-uniqueness of interpolation in image data, which is sampled uniformly in the same two directions, horizontal and vertical, is avoided by always interpolating along these two directions." Good.

Need maybe correct "You can verify that interpolating in the vertical direction first and then in the horizontal direction will yield the same result as Equation 2.14." okay.

Need maybe correct "Figure 2.4. This shows a mesh made of quadrilaterals." okay.

Need maybe correct "However, unlike this case of a uniform planar grid, if this 2D surface happens to be a mesh as in **Figure 2.4**, the result of the interpolation will completely depend on the particular intermediate points you use." okay.

Need maybe correct "Consider the quadrilateral highlighted in red in **Figure 2.4**. Let two opposite vertices have color black denoted by $B$ and the other two vertices have color white denoted by $W$." okay.

Need maybe correct "A point at the intersection of the two diagonals shown by dotted red lines can be interpolated to have two completely different colors." okay.

Need maybe correct "If interpolated from the black vertices, it will be black. If interpolated from the white vertices it will be white." okay.

Need maybe correct "Therefore, there is something special about a triangle, where a point inside it will be interpolated uniquely irrespective of how you do it." okay.

Need maybe correct "This is because a triangle is a simplex. A simplex is a geometric construct achieved by connecting $n$ points to each other in $(n-1)$ dimensions." okay.

Need maybe correct "A straight line is the 1D simplex. A triangle is the 2D simplex (encloses a surface). Similarly, a tetrahedron is the 3D simplex. These are illustrated in **Figure 2.5**." okay.

Need maybe correct "The linear interpolation on these simplices (called bilinear for 2D, trilinear for 3D) yields unique interpolation coefficients which are also called *barycentric coordinates* of a point inside the simplex with respect to the vertices forming the simplex." okay.

Need maybe correct "Therefore **Equation 2.8** provides the barycentric coordinates of the point $V$ with respect to $V_1$, $V_2$ and $V_3$ respectively in **Figure 2.2a**." Good.

Need maybe correct "This is the reason triangles and not any other polygons are chosen for representing geometric meshes." okay.

Need maybe correct "The advantages will be even more evident when we cover computer graphics later in the book." okay.

Need maybe correct "## 2.2 Geometric Intersections" heading. Good.

Need maybe correct "Linear equations represent lines (when using 2 variables) or planes (when using three variables) and we would often need to compute the intersection of such geometric entities." okay.

Need maybe correct "Such intersections are computed by solving a set of linear equations." okay.

Need maybe correct "In order to solve equations with $n$ unknowns, we need at least $n$ equations." okay.

Need maybe correct "First, let us derive a matrix formulation for this problem." okay.

Need maybe correct "Let us consider $n$ linear equations with $n$ unknowns, $x_1,x_2,\ldots,x_n$, where the $i$th equation is given by" then equation. Good.

Need maybe correct "Now, this can be written as" then equation. Good.

Need maybe output.

Need ensure no [PAGE] markers. Good.

Need ensure output in [content]...[/content]. Good.

Let's write final.[content]
![](img/66c45bbed85bb7ba7f7b05dff49b5060_39_0.png)

Figure 2.2. Left: Bilinear interpolation at V from V1, V2 and V3 in a triangle. Right: Bilinear interpolation to find the value of F at P from the value of F at the integer pixels at (i, j), (i + 1, j), (i, j + 1) and (i + 1, j + 1) in an image.

and therefore we are using linear interpolation. Given the locations of the points V1, V2 and V, we can find α by solving the equation

$$x = \alpha x_1 + (1 - \alpha) x_2$$

and use this α to find the value of C(V) from C(V1) and C(V2). The coefficients for V1 and V2 are both between 0 and 1 and their sum is equal to 1.0. Therefore, the function at V is estimated by a weighted sum of functions at V1 and V2 where each of the weights is a fraction between 0 and 1 and their sum is equal to 1. This is called a convex combination of V1 and V2.

If the constraint is only that the sum of the coefficients is 1.0, but the coefficients can be of any value, then it is called an affine combination. If there are no constraints on the coefficients, it is called a linear combination. Note that a linear combination does not always mean linear interpolation. For example, if Equation 2.1 were C(V) = α² C(V1) + (1 − α²) C(V2), it would not be a linear interpolation in α, but would still be a linear combination of C(V1) and C(V2) because α² and (1 − α²) are still scalar values. In other words, for linear interpolation, the derivative of the interpolated function should be a constant.

### 2.1.2 Bilinear Interpolation

Instead of considering 1D data, let us now consider 2D data where the neighborhood of a sample extends in two different directions. Bilinear interpolation entails interpolating in one direction followed by interpolating in the second direction.

For this, let us consider a triangle with three vertices V1, V2 and V3 (Figure 2.2a). To estimate the function C at a point V inside the triangle, we first estimate the function in the two directions V1V3 and V1V2. The point Q on V1V3 is given by linear interpolation as

$$Q=(1-\alpha)V_1+\alpha V_3.$$

Similarly, the point $R$ along $V_2V_1$ is given as

$$R=(1-\beta)V_1+\beta V_2.$$

where $0.0\leq\alpha,\beta\leq1.0$. Therefore $V$ is given by the vector addition of $V_1$, $R$ and $Q$ as

$$V=V_1+((1-\alpha)V_1+\alpha V_3-V_1)+((1-\beta)V_1+\beta V_2-V_1)$$
$$=(1-\alpha-\beta)V_1+\alpha V_3+\beta V_2.$$

Therefore $C$ at $V$ can be estimated as

$$C(V)=(1-\alpha-\beta)C(V_1)+\alpha C(V_3)+\beta C(V_2).$$

Bilinear interpolation also results in a convex combination and the values of $\alpha$ and $\beta$ can be recovered by solving two equations formed by the coordinates of $V$, $V_1$, $V_2$ and $V_3$ in Equation 2.7. Further, you can verify for yourself that the coefficients for finding $V$ do not change if you consider any two different directions like $V_3V_2$ and $V_3V_1$ or $V_1V_2$ and $V_2V_3$ (see exercise for problems on this).

![](img/66c45bbed85bb7ba7f7b05dff49b5060_40_0.png)

**Figure 2.3.** This shows the 4- and 8-connected neighbors in blue for the red pixel in the center.

Now, let us consider bilinear interpolation in another scenario of an image (Figure 2.2b). Any non-integer spatial location may be considered 4-connected when its neighborhood is defined by four nearest neighbors, two in horizontal direction and two in vertical direction. A neighborhood can also be 8-connected when the diagonal neighbors are also included. The distance of the neighbors in the 8-connected neighborhood can be different (for example, diagonal neighbors are $\sqrt{2}$ distance away while the horizontal and vertical neighbors are unit distance away). This is illustrated in Figure 2.3.

Let us consider a function $F$ that defines the color at integer pixels at $(i,j)$, $(i,j+1)$, $(i+1,j)$ and $(i+1,j+1)$ denoted by $A$, $B$, $C$ and $D$ respectively. Let us consider a point $P$ where $F$ has to be estimated as shown in Figure 2.2b. Note that in this case, the location of each of these pixels is defined using 2D coordinates. Therefore, the distance between pixel $(i,j)$ and $P$ in horizontal and vertical direction can be found from their location. Let this be α and β respectively where 0 ≤ α, β ≤ 1. Therefore, the value of F at the pixel Q is given by linear interpolation in the horizontal direction as

$$F(Q) = (1 - \alpha)C + \alpha D \tag{2.9}$$

Similarly the value of F at R is given by

$$F(R) = (1 - \alpha)A + \alpha B. \tag{2.10}$$

Now, the value of F at P is found by interpolating between R and Q linearly in the vertical direction as

$$\begin{aligned}F(P) &= F(Q)\beta + F(R)(1 - \beta) &&\tag{2.11}\\ &= \beta(1 - \alpha)C + \beta\alpha D &&\tag{2.12}\\ &\quad + (1 - \beta)(1 - \alpha)A + (1 - \beta)\alpha B &&\tag{2.13}\\ &= \beta(1 - \alpha)F(i + 1, j) + \beta\alpha F(i + 1, j + 1) &&\tag{2.14}\\ &\quad + (1 - \beta)(1 - \alpha)F(i, j) + (1 - \beta)\alpha F(i, j + 1) &&\tag{2.15}\end{aligned}$$

Now, consider the case where P happens to be on the straight line connecting A and D. In this case, P can be expressed as a linear combination of these two points. The distance AP is given by $\sqrt{\alpha^2 + \beta^2}$ and the distance PD is given by $\sqrt{(1 - \alpha)^2 + (1 - \beta)^2}$. Therefore,

$$F(P) = \frac{\sqrt{\alpha^2 + \beta^2}}{\sqrt{2}}\,D + \frac{\sqrt{(1 - \alpha)^2 + (1 - \beta)^2}}{\sqrt{2}}\,A \tag{2.16}$$

![](img/66c45bbed85bb7ba7f7b05dff49b5060_41_0.png)

Therefore, there are multiple ways to interpolate F at P, using either Equation 2.14 or 2.16, and many more can be found. For example, we may want to interpolate the point at the intersection of AD and BC using A, B and C followed by an interpolation of this point and A to get P. Each of these will result in different coefficients. This non-uniqueness of interpolation in image data, which is sampled uniformly in the same two directions, horizontal and vertical, is avoided by always interpolating along these two directions. You can verify that interpolating in the vertical direction first and then in the horizontal direction will yield the same result as Equation 2.14.

Figure 2.4. This shows a mesh made of quadrilaterals.

However, unlike this case of a uniform planar grid, if this 2D surface happens to be a mesh as in **Figure 2.4**, the result of the interpolation will completely depend on the particular intermediate points you use. Consider the quadrilateral highlighted in red in **Figure 2.4**. Let two opposite vertices have color black denoted by $B$ and the other two vertices have color white denoted by $W$. A point at the intersection of the two diagonals shown by dotted red lines can be interpolated to have two completely different colors. If interpolated from the black vertices, it will be black. If interpolated from the white vertices it will be white.

Therefore, there is something special about a triangle, where a point inside it will be interpolated uniquely irrespective of how you do it. This is because a triangle is a simplex. A simplex is a geometric construct achieved by connecting $n$ points to each other in $(n-1)$ dimensions. A straight line is the 1D simplex. A triangle is the 2D simplex (encloses a surface). Similarly, a tetrahedron is the 3D simplex. These are illustrated in **Figure 2.5**. The linear interpolation on these simplices (called bilinear for 2D, trilinear for 3D) yields unique interpolation coefficients which are also called *barycentric coordinates* of a point inside the simplex with respect to the vertices forming the simplex. Therefore **Equation 2.8** provides the barycentric coordinates of the point $V$ with respect to $V_1$, $V_2$ and $V_3$ respectively in **Figure 2.2a**. This is the reason triangles and not any other polygons are chosen for representing geometric meshes. The advantages will be even more evident when we cover computer graphics later in the book.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_42_0.png)

## 2.2 Geometric Intersections

Linear equations represent lines (when using 2 variables) or planes (when using three variables) and we would often need to compute the intersection of such geometric entities. Such intersections are computed by solving a set of linear equations. In order to solve equations with $n$ unknowns, we need at least $n$ equations. First, let us derive a matrix formulation for this problem. Let us consider $n$ linear equations with $n$ unknowns, $x_1,x_2,\ldots,x_n$, where the $i$th equation is given by

$$a_{i1}x_1+a_{i2}x_2+\cdots+a_{in}x_n=b_i \tag{2.17}$$

Now, this can be written as

$$Ax=b \tag{2.18}$$
