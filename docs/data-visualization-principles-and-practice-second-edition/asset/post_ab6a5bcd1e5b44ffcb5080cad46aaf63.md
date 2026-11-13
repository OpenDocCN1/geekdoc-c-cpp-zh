
and some visual attribute, such as height, position, luminance, or hue. Linear functions are quite effective, since they are invertible, simple to understand, and also preserve distances well between the data and visual spaces. However, linear functions do not work well when the range of distances to be mapped is very large and the data values are not uniformly spread over this range, but clustered in small subranges thereof.

Mapping functions used in visualizations where data is to be measured are sometimes called *measurement mappings* [Lanza and Marinescu 06]. Following measurement theory, a measurement mapping function must fulfill the *representation condition*, which states that such a mapping must “map entities into numbers and empirical relations into numerical relations in such a way that the empirical relations preserve and are preserved by the numerical relations” [Fleeger et al. 05].

In practice, many *Map* functions are, strictly speaking, not invertible over their entire range, and also do not preserve distances. For instance, the shading used in Figure 4.4 to map rainfall values can show only a small number of different values, since both our visual system and the graphics hardware used to render that image can distinguish, respectively display, only a limited set of gray shades. This is not a problem as long as the introduced deviations do not make users draw incorrect conclusions from what they see. As always, evaluations of the effectiveness of a mapping function can only be made with respect to a concrete application domain, task, and user group. To give just a simple example, a colormap that translates scalar values to hues that works perfectly for most people may be quite ineffective for colorblind users.

**Organization levels.** As mentioned earlier, not all visual variables allow equally well the same types of inverse mapping operations. Table 4.1 lists the most common visual variables and their so-called “organization levels” [Bertin 77]. These characterize the types of operations that one can visually perform with ease on such variables. In increasing organization level of detail, a variable $v \in \mathbb{D}_V$ is said to be

- associative if $v$ allows a categorical attribute mapped by $v$ to be perceived independently on the presence of other visual variables in the same image. For instance, “shape” is associative, since we can easily distinguish different shapes even when colored or positioned differently. A variable that is not associative is called *dissociative*;

- selective if $v$ allows a categorical value mapped by $v$ to be (nearly) instantaneously perceived as different from other values mapped by $v$. For instance,

| Visual variable | Quantitative | Ordinal | Selective | Associative/Dissociative |
|---|---|---|---|---|
| Position | ✓ | ✓ | ✓ | A |
| Size | ✓ | ✓ | ✓ | D |
| Brightness | | ✓ | ✓ | D |
| Texture | | ✓ | ✓ | A |
| Color (hue) | | ✓ | ✓ | A |
| Orientation | | | ✓ | A |
| Shape | | | ✓ | A |

Table 4.1. Organization levels of visual variables.

"color" is selective, since we can easily visually select all red shapes in a set of differently-colored objects;

- ordinal if $v$ allows one to pre-attentively compare different values mapped by $v$. For example, "size" is ordinal, since we can easily see if two objects have the same size or if one object is larger than the other one;
- quantitative if $v$ allows one to visually compute ratios between different values mapped by $v$. For example, "size" (seen as length, for instance) is quantitative by excellence, since we can easily tell how many times an object is longer (or shorter) than another object.

The properties of the organization levels outlined in Table 4.1 are, of course, not granted. These are properties that a given visual variable _can_ take, given a well-designed visualization and taking into account an average use-case and user. We can clearly find cases when these properties do not hold, due, e.g., to a poor visualization design, a too-large dataset, a bad display device, or an untrained or inattentive user. The main value of this classification is to render designers aware of the inherent limitations that visual variables have. For instance, because "size" is (typically) quantitative but "color" is not, displaying a data attribute for which we wish to visually compute and compare ratios should best map this attribute to size rather than color.

Related to the inversion process is the difference between _data_ and _information_. Following the discussion of Spence [Spence 07], we state that the main task of visualization is to derive information, i.e., useful facts that lead to conclusions about a certain problem, from data, i.e., recorded figures such as the signal samples on a grid. The mapping function should allow retrieval of information, and not just raw data, from the produced pictures.

Further reading. Designing effective visual mappings is at the core of the success (or failure) of designing effective visualization applications. Besides the basic theory covered in this section, many more aspects contribute to a successful design: choice of visual encodings as a function of the display medium; accepted conventions of the targeted user group; usage of interaction mechanisms to facilitate data exploration; knowledge of perceptual, cognitive, and human vision factors; and aesthetic principles driving the overall visualization design. More information on the above topics is available in a variety of places. The recent book of Ward et al. provides a thorough and balanced coverage of all the above points, with a focus on interactive visualization and user-centered design [Ward et al. 10]. The classic book of Tufte provides a lower-level, but equally important, view on the design of statistical graphics [Tufte 01]. Chapter X in the Visualization Handbook of Hansen et al. provides additional insight in perceptual issues in data visualization [Hansen and Johnson 05]. Finally, the books of Bertin provide a detailed discussion of the desirable properties of visual variables used in the design of the mapping function and how these should be used to encode different types of attributes [Bertin 77, Bertin 83].

## 4.1.4 Rendering Data

The rendering operation is the final step of the visualization process. Rendering takes the 3D scene created by the mapping operation, together with several user-specified viewing parameters such as the viewpoint and lighting, and renders it to produce the desired images:

```
Render : \mathbb{D}_V \rightarrow \mathbb{I}.
```

In typical visualization applications, viewing parameters are considered part of the rendering operation. This allows users to interactively navigate and examine the rendered result of a given visualization by rendering the 3D scene without having to recompute the mapping operation. Indeed, if the viewpoint changes but the 3D scene produced by the mapping stays the same, all we have to do is render the scene anew with the new viewing parameters, which is a relatively cheap operation.

## 4.2 Implementation Perspective

Putting it all together, we can describe the visualization pipeline as a composition of functions that have dataset arguments and values. If we denote by \mathbb{D} the space of all our datasets then we have

```
Vis = F_1 \circ F_2 \circ ... \circ F_n, \quad where \quad F_i : \mathbb{D} \rightarrow \mathbb{D}.
```

The various functions \( F_i \) perform the data rendering, mapping, filtering, and importing, thus in inverse order of their appearance in the visualization pipeline. The input of \( F_n \) is the application's raw data, and the output of \( F_i \) is the final image. This model allows us to decompose each of the four stages into as many subfunctions as we need. This has several purposes. First, it is conceptually easier to think of complex operations, such as filtering, in terms of a composition of simple filter-like atomic operations that each address a specific task. Second, this favors modular, reusable software design and allows us to assemble visualization applications from a set of predefined functional components. In practice, there is no clear-cut separation as to which functions should be considered in the data importing, filtering, mapping, and rendering stages. Different visualization applications make different choices here. From a purely implementation perspective, all data types used in the pipeline (raw data, sampled datasets, and images) can be considered as datasets, and all pipeline operations can be modeled as functions that read and write datasets.

The design of a visualization application has two main parts. First, we choose the right data-processing operations, or functions \( F_i \), that are needed in the visualization pipeline of a given application (see Equation (4.7)). Second, we choose the right dataset implementations \( D_j \in \mathbb{D} \) to connect the pipeline functions \( F_i \). We outlined in Chapter 3 how to implement the datasets \( D_j \). We now briefly discuss how to implement the data-processing operations \( F_i \).

Dataflow design. If we use an object-oriented design, we can implement the functions \( F_i \) as classes that have three properties:

- They read one or more input datasets \( \mathcal{D}_i^{\text{inp}} \).
- They write one or more output datasets \( \mathcal{D}_j^{\text{out}} \).
- They have an execute() operation that computes \( \mathcal{D}_j^{\text{out}} \) given \( \mathcal{D}_i^{\text{inp}} \).

The choice of letting the function \( F \) have several datasets as input (arguments) and output (results) is purely a practical one. The actual number, type, and meaning of the inputs and outputs depends on the semantics of the function itself. In implementation terms, a function \( F \) with these properties can be modeled as a class F with three methods as shown in Listing 4.1. The setInput() and getOutput() methods are simple accessors to the input and output datasets \( \mathcal{D}_i^{\text{inp}} \) and \( \mathcal{D}_j^{\text{out}} \), respectively. These are represented by Grid subclasses, such as uniform or unstructured datasets, which have been detailed in Chapter 3. In a basic implementation, the accessors would simply store references to the input and output datasets in the local inputs and outputs vectors of the F
