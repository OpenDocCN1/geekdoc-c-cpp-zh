
We also need to make a floor for the ball to bounce on. This consists of a grid that is the same width as our shed and is long enough to fit all of our ball bounces on (5 units × 40 units). This only has to be built once. It can be reused for each ball we animate.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_112_0.png)

Then we need to make our balls. These will all be the same size? We want an audience to be able to tell what sort of ball they are from their movement rather than their size. The balls will always be 1/5 the size of the width of the shed.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_112_1.png)

Each of the balls will have to be constructed with a 'hierarchy.' A hierarchy is an abstract graphical interpretation of how a model is constructed. It consists of a 'parent' that could then be linked to any number of 'children.' Let's say we have two objects on screen, a big cube and a smaller cube. They will be linked together in a hierarchy. The large cube is the parent and the smaller cube is the child. When you select the large cube (the parent) and move it, the small cube (the child) will move with it. But, when you select and move the small cube (the child), it will move on its own, leaving the large cube (the parent) behind.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_113_0.png)

Movement given to the parent will affect all of the children, but movement given to a child will work independently of the parent.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_113_1.png)

Once the movement key positions are in place, the computer will do the in-betweens for us. As we saw in Chapter 1, the in-betweening that the computer does will not be correct. We have to tell it where to put the in-between balls. We do this either by putting in all the in-between balls ourselves or by manipulating the animation curves, as in Chapter 1.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_115_0.png)

Once the movement is done we can go back over our animation and set keys for rotation on the rotation part of the hierarchy. Select the rotation part of the hierarchy and set a key at the very start of the piece of animation. Work out how much the ball will rotate over the length of the scene by measuring the distance travelled in relation to the circumference of the ball. Then, go to the very end of the scene, rotate the ball by the correct amount and adjust the curves to make it look right.

## The Construction of a Simple Character, its Articulation and Balance

### Chapter Summary

- Basic Human Anatomy
- Joints
- Movement in Arcs
- Line of Action
- Designing a Basic Human Character
- How to Design a 3D Character
- Overview of How to Build and Rig a Simple 3D Character
- Planning a Scene
- Animating Your Characters (Using the Left and Right Sides of the Brain)
- Exercises

Animating inanimate objects such as bouncy balls gives you an idea of weight, timing, spacing, and squash and stretch. However, they are not the most interesting things to animate. During this chapter, we will animate something with life, something that initiates movement and has forces imposed upon it: the human character.

Our first task is to design our character. Before doing this we need a basic understanding of human anatomy. I will go through the construction of the skeleton and types of joints. As well as looking at the structure of these, I will also explain how they move and the importance of arcs when animating.

### Basic Human Anatomy

A whole book could be (and likely has been) written on animating human and animal anatomy, so I’m going to stick to the absolute minimum that we need to know. Let’s start with the main part of the human skeleton: the spine.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_117_0.png)

#### The Spine

At the center of the human skeleton is the ‘S’-shaped spine. It is made up of 24 individual bones, called vertebrae, which are linked by discs of cartilage. This combination gives the spine great flexibility, allowing forwards and backwards and side-to-side movement and a degree of twisting.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_117_1.png)

At the top of the spine are the seven vertebrae that make up the neck.

#### The Rib Cage

Attached to the next twelve vertebrae are 24 ribs (two per vertebra), which constitute the rib cage. The role of the rib cage is to protect the heart, lungs and internal organs. At the bottom of the rib cage is the diaphragm; this, in conjunction with the rib cage, controls breathing. The rib cage restricts the bending and twisting movement of the 12 vertebrae that the ribs are attached to. The lower five vertebrae make up the lower spine. Most of the twisting and bending of the spine during the body’s movement occurs between these five vertebrae.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_118_0.png)

#### The Pelvic Girdle

![](img/49afe0fca1d8f7ebd02f6839692b55f6_118_1.png)

At the base of the spine is the pelvic girdle. This solid set of bones plays a role in keeping us upright. Attached by ball and socket joints are the two femurs of the upper legs. The largest muscle in the body (the gluteus maximus) is attached to the upper thigh bone (the femur) at one end and to the pelvic girdle at the other end. This muscle is used to hold the body upright when stationary and moves the femur during walking. It is used when picking things up and jumping. It also helps with the balance of the body.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_118_2.png)

The shoulder blades are almost free-floating and can move in a number of directions: up and down, inwards so that they are almost touching at the spine and outwards to the edge of the rib cage. The main things restricting their movement are the collarbones.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_121_0.png)

The movement of the shoulder blades affects the position of the arms. For example, by raising the shoulder blades, the arms raise and give the body the appearance of a shrug. When picking up a heavy object, the shoulder blades and collarbones will be lowered, lowering the position of the arm. Much of the character and mood of a person is conveyed by the positions of the shoulders. See ‘shoulderjoint.avi’, Chapter 3 on the website.

### Joints

The limbs of the skeleton are linked by joints, of which there are six types. These are:

- 1. Plane joints
- 2. Pivot joints
- 3. Hinge joints
- 4. Ball and socket joints
- 5. Saddle joints
- 6. Condyloid joints

Understanding how these joints work gives us a clue to understanding movement.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_121_1.png)

![](img/49afe0fca1d8f7ebd02f6839692b55f6_121_2.png)

#### Plane Joints

The surfaces that meet at a plane joint are flat or slightly curved. This allows only a small amount of movement: about 90 degrees backwards and forwards and approximately 45 degrees from side to side. Examples are the wrist and ankle. See ‘plane-joint.avi’, Chapter 3 on the website.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_121_3.png)

### Movement in Arcs

As an experiment, I built a human character in 3D. Rather than giving it skin, I put a white ball at each of the joints. Set against a black background, all you see is a collection of white spheres. I then animated a basic walk cycle, with the character walking on the spot. When the animation plays, all you can see are some white balls moving through space. Despite the abstract nature of the sequence, it is surprisingly easy to work out that it is a human character walking on the spot. This emphasises how important it is to be mindful of reality when moving human characters. Take a look at ‘arcs.avi’ in Chapter 3 on the website and see if you can work out whether it’s a person walking or not.

![](img/49afe0fca1d8f7ebd02f6839692b55f6_124_0.png)

When somebody looks to the side, their head will bob down through an arc. When somebody jumps in the air, his or her trajectory will describe an arc. Almost all movements made by any living thing will follow an arc. If the character doesn’t follow arcs with its movement, your animation can look stiff and robotic.
