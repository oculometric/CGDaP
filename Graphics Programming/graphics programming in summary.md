
# Coordinate Systems and 3D Space
A coordinate system is just a way of representing transformations in a particular coordinate space. That might seem like a circular definition, but roll with it for a minute. This section covers important stuff about what vectors and matrices are, how they interact, and how those mathematical building blocks are combined to implement the 3D world in games. Brace yourself for a detour into matrices.

In our 3D, we represent our dimensions as the sum of three different axis vectors, the $X$ axis, $Y$ axis, and $Z$ axis. By default these have the values: $$X = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix}, Y = \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix}, Z = \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix}$$
This might seem redundant but it is a useful concept.
Thus we define a point in 3D space as having X, Y, and Z components. Let's define a point $p=\begin{bmatrix} 1 \\ 4 \\ 3 \end{bmatrix}$. We can say for this that $p = 1X + 4Y + 3Z$, where $X$, $Y$, and $Z$ are our axis vectors.

### Vectors
The follow-up question to this is *"what is a vector?"*. Conceptually, **a vector is a line between two points**, and is represented by the distance between those points as specified by individual $XYZ$ components (i.e. it has direction and magnitude, ayyyy). So a vector has the same structure as a point: three numbers, one for each axis. Conversely, we can also say that **a point is really just a vector which starts at the origin** (and ends at the point). This gives a bit more context to the idea that a point is represented by a sum of the three axis vectors.

I also want to introduce the concept of a **unit vector**, which is a vector which has a **magnitude** of $1$. **Normalisation** is the process of forcing a vector to have length $1$, by dividing all of it's components by it's magnitude, and is where the term 'normal vector' comes from.

### Magnitude of a Vector
Let $v$ be some vector, then the magnitude of $v$ is given by $$|v| = \sqrt{(v.x)^2 + (v.y)^2 + (v.z)^2}$$
### Dot Product Between Two Vectors
Let $v$ and $w$ be vectors. The dot product between them is given by $$v\cdot w = (v.x \times w.x) + (v.y \times w.y) + (v.z \times w.z)$$
In words, you multiply each element in the first vector by its corresponding element in the second, and add the results of all those multiplications together.
Your result is a single (scalar) value.
Dot products follow the identity
$$v\cdot w = |v||w|\cos(\theta)$$
where $\theta$ is the angle between the two vectors.
The dot product can be extended to higher dimensions (and lower ones). The input vectors in a dot product can be swapped around (they are commutative)
$$v\cdot w = w \cdot v$$

### Cross Product Between Two Vectors
Let $v$ and $w$ be vectors. The cross product between them is given by $$v\times w = \begin{bmatrix} (v.y \times w.z) - (v.z \times w.y) \\ (v.z \times w.x) - (v.x \times w.z) \\ (v.x \times w.y) - (v.y \times w.x) \end{bmatrix}$$
The result of this is a *vector* of the same dimension as the input vectors.
Cross products follow the identity
$$v\times w = |v||w|\hat n \sin(\theta)$$
where $\theta$ is the angle between the two vectors and $\hat n$ is a vector which is *perpendicular* to both of the input vectors and has a magnitude of $1$.
The cross product cannot be generalised to higher/lower dimensions (at least, not in quite the same way that dot products can). It is also not commutative (if the input vectors are swapped, the result is negated)
$$v \times w = -(w \times v)$$
<TODO: diagram of cross product handedness>
### The Origin
In a previous paragraph we said that a point is conceptually a vector which starts at the origin. Well, *what happens if we move the origin?* If we do that, then we're effectively creating our own **coordinate space**. All our points are still measured from the origin, and described by a set of three axis vectors, so if we change the definition of the coordinate space by moving, rotating, or scaling that origin, **we are effectively applying the same set of transformations to all the points defined within that space**.

Here is as good a place as any to emphasise that all coordinate systems are relative. For instance, it doesn't actually matter which axis you treat as the 'up' axis, whether it's $Z$, $Y$, or even $X$, *as long as you're consistent within your software, it doesn't matter*. I don't wish to make this existential but coordinate systems are really just a useful concept for concretising an abstract non-existent space with numbers, and as long as you handle those numbers consistently, you can kinda do whatever you want.

Likewise, moving the origin doesn't really mean anything if everything else is also relative to that origin. If you move the world origin in your 3D scene, then you're moving your camera by the same amount as you're moving the geometry and everything else, so to all intents and purposes, nothing has changed.

### Transforming Between Coordinate Spaces
In 3D graphics we mostly are talking about 3 different coordinate spaces, which here I'll call **Object Space** (aka local space, model space), **World Space** (aka global space), and **Camera Space**. Let's set the last one aside for now and consider object and world space.

Imagine we have an object, a 3D model consisting of a series of points. Those points are each represented by a `Vector3`, i.e. a vector from the *model's* origin. Now, *how do we rotate and move that model in our scene, and have all it's points move with it?* Well, if we figure out how those transformations affect the origin and axis vectors for the object's space, then we can apply those to each point in the object.

For instance, if we rotate the object by 90 degrees around the Z axis, then our axis vectors will change from being
$$X = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix}, Y = \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix}, z = \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix}$$
to become
$$X' = \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix}, Y' = \begin{bmatrix} -1 \\ 0 \\ 0 \end{bmatrix}, Z' = \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix}$$
Notice how the axis vectors have changed. Now, lets say we have a point $p$ which we define to have the position $p=\begin{bmatrix} 2 \\ 6 \\ 3 \end{bmatrix}$ in **object space** (meaning relative to the object's origin and axes). Well, to find it's position in **world space** we need to consider that $p.x = 2$ actually represents *"go 2 units along the object's X axis vector"*. Thus, to find $p$'s **world position**, we can multiply each component in $p$ by its corresponding axis vector and add the results. $p'$ is going to be the position of our point in **world space**:
$$p' = (p.x * X') + (p.y * Y') + (p.z * Z')$$
$$p' = 2\begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix} + 6\begin{bmatrix} -1 \\ 0 \\ 0 \end{bmatrix} + 3\begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix}$$
$$p' = \begin{bmatrix} -6 \\ 2 \\ 3 \end{bmatrix}$$
If we want to translate our object as well as rotating it (translate just means moving it), then we can simply add on the vector representing our translation.

### Order Matters
A problem you might encounter is exactly what order these transformations are applied in. The key point to remember is that *transformations are always applied relative to the origin*. If you rotate something, you rotate it around the origin. If you translate it, you translate it relative to the origin. If you scale something, you scale it around the origin. This means that if you have an object which needs to be rotated and translated (i.e. it has a position and rotation in the world), then you need to rotate it first, then translate it:
<TODO: diagram of why order matters>

### Transformation Matrices
Now is where things can get a bit scary. I'm not going to go into detail on exactly what matrices do, but I want to explain what they are and how they're used in this context.

First of all, we need to introduce 4D matrices, or 4x4 matrices (and associated `Vector4`s). We're not actually going into four dimensions, but we are using that fourth component for a particular purpose, which you'll see. The advantage of using 4x4 matrices is that we can combine an entire transformation between coordinate spaces (scale, rotation, translation) into a single matrix.

The transformation we applied above, rotating a point about the origin, we applied using some manual mathematics, multiplying each component against it's corresponding axis vector. Well guess what! Mathematicians can do that for us!

### Matrix Multiplication With a Vector
This section you can maybe skip over. It's important if you really want to understand why matrix multiplication is so useful. You don't need to actually remember the maths for this.

Let $v$ be a vector with four components, $v = \begin{bmatrix} x \\ y \\ z \\ w \end{bmatrix}$
Let $m$ be a matrix of dimension 4 by 4, $m=\begin{bmatrix} a & b & c & d \\ e & f & g & h \\ i & j & k & l \\ n & o & p & q \end{bmatrix}$
Multiplying $v$ by $m$ gives the following result:

$$m \cdot v = \begin{bmatrix} a & b & c & d \\ e & f & g & h \\ i & j & k & l \\ n & o & p & q \end{bmatrix} \cdot \begin{bmatrix} x \\ y \\ z \\ w \end{bmatrix}$$
$$m\cdot v = x\begin{bmatrix} a \\ e \\ i \\ n \end{bmatrix} + y\begin{bmatrix} b \\ f \\ j \\ k \end{bmatrix} + z\begin{bmatrix} c \\ g \\ k \\ p \end{bmatrix} + w\begin{bmatrix} d \\ h \\ l \\ q \end{bmatrix}$$
From here it's just scalar vector multiplication and vector addition, but importantly, *you can see the same structure emerge as we saw when rotating a point*. The vector we multiply $x$ by **is the X axis vector**, etc for Y and Z. The $w$ component of the vector $v$ is always set to $1$, so our $d,h,l,q$ values are constants that get added on regardless of the rest of the vector (e.g. for translation operations).

### Back to Transformation Matrices
We can relatively easily construct matrices representing transformations, and when we multiply the matrix and the point together as above, this transformation is being 'applied' to that point.

Now, when you multiply matrices together with one another (I'm not writing the maths for that out) we need to know two things:
1. matrix multiplication is associative
2. matrix multiplication is **not** commutative
This means that, assuming $a$, $b$, and $c$ are all matrices
$$(a\cdot b) \cdot c = a \cdot (b \cdot c)$$
$$a \cdot b \not = b \cdot a$$
This reinforces that the order of transformations matters. However, it means that we can combine matrices for translating, rotating, and scaling, into a single 'transformation matrix' by multiplying the individual translation, rotation, and scaling matrices together. If we come up with a matrix $t$ for translating, $r$ for rotating, and $s$ for scaling, then we can combine them into one $m$ matrix like this
$$m = t \cdot r \cdot s$$
Remember that when we transform a point $p$, we *pre*multiply by $m$ so doing
$$p'= m \cdot p $$
we're effectively doing
$$p' = t\cdot (r\cdot (s\cdot p))$$
That is to say, the rightmost thing is applied first: scale, then rotation, then translation.

Hopefully that all made sense. Now it's back to coordinate space transformations!

### Back to Coordinate System Transformations
Now you've seen the wonders of matrices, you understand that we can do pretty much any transformation imaginable with 4x4 matrices and `Vector4`s. You've also seen that we can combine matrices together to create a single transformation from several smaller ones.

Looking back at the **object** and **world** spaces, *how do we comprehensively transform a point from object space to world space?* Well, we create a transformation matrix which represents how the object's axes differ from the world's axes. The object might be scaled in different amounts along the X, Y, and Z axes, it may have rotations around any of these axes, and it may have been translated as well. We can combine those operations into a single matrix which represents the *transformation from object space to world space*: the **object-to-world** matrix. Which answers the question of *"if this is where the point is in object space, where is it in world space?"*.

Now let's talk about the camera.

### The Camera
Okay, nearly there. *"How does the camera fit into all of this?"* Well, for the next step in the rendering pipeline, projection, we want all of our points and other 3D stuff to be *relative to the camera*. If you understood the stuff about vectors and spaces above, you're now saying to yourself, *"aha! so we need a matrix which transforms points from world space into camera space!"*, and you'd be completely correct to think that. Well done, you're very smart for thinking that.

So how do we do that? Well, pretty much the same way as for any other object, except with a slight caveat. Let's compute a matrix the same way as we did for our object above, and call it $m$. What does $m$ represent? It represents the **camera-to-world** transformation. However, we've already got stuff in world space, we want the opposite, we want the **world-to-camera** transform instead. Luckily, matrices are really clever, so we can simply find the inverse of the **camera-to-world** matrix, and use that! The same can be done by simply doing the opposite transformations (i.e. rotate by $90$ degrees becomes rotate by $-90$, scale by $1.5$ becomes scale by $1/1.5$, translate by $100$ becomes translate by $-100$) in the opposite order.

This now gives us all our points expressed as positions relative to the camera's origin, with the camera's rotation and scale also applied.
> If you're interested, conceptually what this represents is that we take all the stuff in the scene, including the camera, and move it/rotate it/scale it such that the camera is at the world origin, with no rotation and no scale.

Congratulations, we did it! We made it to camera space!

### About Camera Orientation
<TODO: this>

### One More Note
Since we can combine matrices together to create compound transformations for a single object-to-world transform. However, we can also combine those into even more compounded transformations. If you have nested objects, 'objects within objects', and you want to get from the sub-object space into world space, you first apply the object's transformation, then the sub-object's transformation. You can imagine it like you're peeling the layers off of an onion. Apply the outer object transform, and everything on that layer is now in world space. If there's another layer (a child object), apply its transform to all of its children, and then they're in world space too. Repeat until you've reached the bottom of the chain. Shrek would be so proud rn.

# Projection: Perspective and Orthographic
model/object coords --modelview matrix--> eye coordinates --projection matrix--> clip coordinates --perspective division--> NDCs --viewport transformation--> window coordinates.
// TODO

# Geometry (dun dun duuuun)
In this section I'm going to talk about geometry in the narrow, triangle-mesh sense. However, there are other ways geometry can be expressed, lots of ways in fact, but they require cleverer algorithms and aren't what we're focussing on with this module.

A **triangle mesh** is composed of **triangles**, that's obvious. *Why?* Because triangles are the simplest 3D shape, they are guaranteed to be flat (think of a chair with three legs: there's no way to have one leg too short!), and doing maths with them is easy.

**Triangles** are bounded by **edges** which are composed of **vertices**. A triangle having three corners means it has three vertices.

When storing a triangle mesh, the first way to think about it is as a list of **triangles**, each of which contains three points, each of which contains three coordinates (so 9 numbers in total per triangle). However, the vast majority of those points are going to be shared between two or more triangles, so it makes much more sense to store the vertices elsewhere. Thus version two of our data storage consists of two lists:
- A list of triangles, each of which contains three numbers, which are indices into the second list
- A list of vertices, each of which contains three numbers, which are its coordinates in object space
So a triangle might be defined as `{0,1,2}` which means, look at the first, second, and third items in the vertex list, and make a triangle between those three points.

<TODO: rendering a triangle mesh?>

However, there's more to a mesh than just its geometry. *What about normals?*

### Normals
You've almost certainly heard of them before but let's define them here in a couple of different ways.
**Definition #1: a vector with magnitude 1**
Pretty self explanatory. A vector where the magnitude doesn't matter, and we can focus on it's direction instead.
**Definition #2: the direction a surface is pointing**
Normals are used to represent the direction a surface is facing in. Imagine lying down on your back on a particular triangle: the direction of your eyes, directly out of the surface, is the normal vector. The normal vector is always perpendicular to the surface it is the normal to.

Normals are useful for various things: you can determine if you're looking at the back or the front of a surface based on the angle between the viewing vector (the direction you're looking in) and the normal vector using the dot product formula; and you can use them for lighting calculations. We'll talk more about that later.

In order to 'normalise' a vector, you just divide all of its components by its magnitude (i.e. the resulting vector has magnitude $1$):
$$\hat v = \frac{v}{|v|}$$

Now, you can calculate the normal of a triangle very easily, as below:
```
// These three vertices describe our triangle
Vector3 vertex_a = {0.4f, 0.2f, 1.0f};
Vector3 vertex_b = {1.2f, 3.2f, 1.0f};
Vector3 vertex_c = {1.4f, 0.8f, 1.5f};

// Calculate vectors a->b and a->c
Vector3 vector_ab = b - a;
Vector3 vector_ac = c - a;

// Calculate the cross product between ab and ac, and normalise it
Vector3 normal = normalise(cross(ab, ac));
```
And now we have our normal vector. Mathematically what we just did was find two vectors which lie in the plane of the triangle ($\vec{ab}$ and $\vec{ac}$) and cross-producted them to find a vector which was perpendicular to both (and thus perpendicular to the plane), and then normalised the result.

Now, knowing what way a flat triangle is facing is all good, but it isn't always what we want. We may want to define custom normals for individual vertices, in order to give our mesh a smooth, rounded-looking surface (without actually cutting it up into millions of tiny triangles). These **vertex normals** are then interpolated over the triangle, which we'll talk about further down.

This introduces an issue with our two-list model of mesh data however, since a vertex might have multiple *different* **vertex normals** when it occurs in different triangles.
<TODO: multiple vertex normals diagram>

The solution to this is to add another list, and to separate **vertices** from **face corners**.

### Face Corners
A face corner is exactly that: the corner of a face (in this case, all our faces are triangles). Multiple **face corners** may reference the same **vertex**, but have differing data on other fronts.

Let's make a version three of the mesh storage model. For this, I'm going to call the number of **vertices** $v$ and the number of **triangles** $t$.
- A list of vertex indices which make up triangles (this list is $3\times t$ items long)
- A list of vertices each of which is a `Vector3` (this list is $v$ items long)
- A list of vertex normals each of which is a `Vector3` (this list is $3\times t$ items long)

This way, every **face corner** can have a unique **vertex normal**, but can also share its **vertex** data.

### Texture Coordinates (UVs)
We also want to store texture coordinates (also called UV coordinates or just UVs) alongside our vertex data, so let's introduce an extra list for this (we'll talk about texture coordinates below). UV coordinates are also **face corner** data, since multiple faces sharing the same **vertex** might want to have different **UV coordinates**.

Our final mesh format looks like this (again the number of **vertices** is $v$ and the number of **triangles** is $t$):
- A list of vertex indices which make up triangles (this list is $3\times t$ items long)
- A list of vertices each of which is a `Vector3` (this list is $v$ items long)
- A list of vertex normals each of which is a `Vector3` (this list is $3\times t$ items long)
- A list of texture coordinates each of which is a `Vector2` (this list if $3 \times t$ items long)

### Winding Order
Let's revisit the normal vectors from before. We mentioned that the normal vector is used to determine which side of a face is the front and which is the back. This becomes quite important when we're talking about lighting and backface culling (again, more on this below). The formula for the normal vector of a triangle looks like this (mathematical format instead of code this time):
$$\hat n = \frac{(b-a) \times (c-a)}{|(b-a) \times (c-a)|}$$
Now, we've defined our triangle to have the vertices `{a,b,c}`, in that order. *However, what happens if we swap `b` and `c`?* Well, we find that our cross product gets inverted, and points in the opposite direction. We have discovered **winding order**.

**Winding order** refers to the ordering specification of our vertices. A **counter-clockwise** winding order means that when you're looking at the front of a face, the vertices are numbered counter-clockwise. You can guess how it is for a **clockwise** winding order.

<TODO: diagram of clockwise/counter-clockwise winding orders and their normals>

# Interpolation and Barycentric Coordinates
In a general sense, interpolation is the process of guessing how stuff should look based on two values and how far you are between them. For instance, if we have a line with a '1' mark at one end and a '5' mark at the other, we could subdivide the distance between them with other numbers (2-4, equally spaced). This is, in it's simplest form, interpolation.

We can describe interpolation in **one dimension** mathematically, with a fairly simple formula. Let's let $A$ be the first value and $B$ be the second value. We're also going to define $x$, which is how far along the line from $A$ to $B$ we are as a fraction:
$$C = xB + (1-x)A$$
Essentially we're taking some of $B$ and some of $A$. When $x=0$, we just get $A$. When $x=1$, we get $B$. Anything between those two and we get something between $A$ and $B$. If we allow $x$ to go outside the $0..1$ range, we're doing extrapolation, which is useful sometimes.

> It's worth keeping in mind that $A$ and $B$ don't have to just be numbers. They can be `Vector2`s, `Vector3`s, etc. As long as you can perform scalar multiplication and component-wise addition, you can do this kind of interpolation, since you're really just performing interpolation on each individual component of your vector, and recombining them at the end.

Interpolation is really useful for filling an area with a gradient (among many other things), because it lets us **blend** between two discrete values to create a continuous field of values. Interpolation may also be called **lerping** (linear interpolation; there are other types of interpolation actually) or **blending** or **mixing** (only in certain contexts).

A specific example of this is with **texture coordinates**. In the last section we talked about how we can attach UV coordinates to face corners, and we'll talk more about what those coordinates do later on. In order to meaningfully texture the face of an object, we need to know the UV coordinate of not just the three corners of a triangle, but for every point within that triangle. Thus, we need to interpolate between the texture coordinates given at the face corners based on where we're looking in the triangle. *"How do we do that if we have three values to work with, not two?"* Enter, **barycentric coordinates**.

<TODO: barycentric coords>

# Textures and Texture Coordinates

# Lighting and Materials
Usually we want to do something interesting with 3D models, and thus we need to light them somehow.

### In the Real World
Light in the real world travels in little packets, photons, which can be absorbed, reflected or refracted by surfaces and materials. Let's not think about refraction or any quantum mechanics bullshit, and focus on the absorption and reflection bit.
Materials will reflect or absorb photons based on their wavelength and the properties of the surface:
> A red surface under a white light means that the surface is absorbing all wavelengths except the red ones

### In Computers
In computers, we can use multiplication to represent this absorption/reflection of light. Since the colour of the surface and the colour of the light are each represented by a set of three floating-point, RGB values (a `Vector3`):
> A white light, `Vector3{ 1.0f,1.0f,1.0f }` shining on a red surface, `Vector3{ 1.0f, 0.0f, 0.0f }`, means that the surface colour is being multiplied by the light colour to produce the resulting red

Doing things like this means that we can change the light colour and it will appropriately affect the surface. For instance, if the light colour contains no red light, and the surface only reflects red light, then the surface will appear black as we'd expect. If the light colour is less bright, then the surface red will also appear a darker red.

### Why Are We Using Floating Points
Most **colour** representations describe colours with three components (**red**, **green**, and **blue**) which can vary between $0$ and $255$. This is useful when we're talking about storing image colours with a single **byte** for each component. However, when we want to do maths with colours, we use **floating point** numbers instead, saving division at every single step in our calculations. Less efficient to store, but easier (and **more precise**) to work with.

### Lighting A Scene
In reality, a photon might bounce back and forth between hundreds of surfaces before reaching the viewer. That means lots of maths, and raytracing which is *very slow*. We won't go into detail about more complex lighting schemes which try to emulate this, but these are called **global illumination**, the idea being that everything can cast light and shadows against everything else in the scene. What we're looking at instead is **local illumination**.

Local illumination is a calculation performed usually in the **fragment shader** (see below), meaning it's being evaluated per-pixel for a surface. This **shading** is calculated by taking into account different material parameters and different lights. Multiple lights may affect a single surface, and their light contributions are added together (again, this is how light behaves in the real world).

Lighting a surface is a mathematical affair. There are lots of complex surface lighting models, but for realtime lighting like this, we use a model called **Phong lighting**, which separates light contribution into three parts:
1. Diffuse - this is light which reflects in all directions when it hits a surface. This kind of shading depends on the angle at which the light ray hits the surface (if it hits at a more oblique angle, the light energy is being spread out over a greater area, and thus appears less bright). This kind of shading also depends on the distance to the light source (the inverse square law tells us that as the distance to the source doubles, the area over which the light energy has to spread quadruples, and thus the light energy delivered per area is quartered)
2. Specular - this is light which reflects in a particular direction (specifically it is reflected in the normal vector of a surface) when it hits a surface. This shading depends on the angle between the light ray and the surface, and the angle between the viewer and the reflected ray (the maximum brightness is achieved when the viewing ray is identical to the reflected ray, i.e. we're looking directly into the reflection of the light source). This kind of shading is also affected by the distance to the light source, as above. Importantly, this kind of shading is also affected by an attenuation factor of the surface, which controls how concentrated the specular reflection is (more concentrated reflection appears as a smaller, brighter spot, as if it were a smoother, shinier surface)
3. Ambient - this is light which just exists magically in the world, travelling in all directions from all points, and thus gives the surface some light contribution no matter where that surface is or the direction it's facing
The fourth, more sinister form of shading (which is not part of Phong illumination) is emissive shading which involves adding some extra colour to a surface.

In order to evaluate the colour of a pixel involves evaluating the light contributions for different kinds of lighting. We multiply the incoming light ray colour with by different factors for the diffuse, specular, and ambient contributions, and then by the *colour which the material provides for those different forms of shading*, and finally we add the results of all of those. The equation for this might take a form like this:

Shaded colour $=$ $($light colour $\times$ diffuse colour $\times$ normal direction$\cdot$ray direction$) + ($light colour $\times$ specular colour $\times$ reflected direction$\cdot$view direction$) + ($light colour $\times$ ambient colour$)$ $+$ emissive colour

I know that looks like a mess, and it's fairly simplified, but it should give you an idea of how lighting is calculated. Perform that equation for each different light to calculate their individual contributions, and then add them all together to get the overall surface colour.

Some lighting systems will also let you separate the colour contributions at the **light source** level: as well as specifying diffuse, specular, and ambient colour factors on each material, you can specify them on the light source as well, and corresponding factors will be multiplied together (light diffuse with material diffuse, etc etc).

<TODO: diagrams needed>

# Aliasing and Culling
Ok so we know what meshes are and what they're (usually) made of. *"Why would we want to cull parts of them?"* Well, a few reasons:
1. Performance. It's pretty self-evident that if you can eliminate half of the triangles in the world before you even start doing other maths on them, you can save a lot of time
2. Aesthetics or effects. Some games deliberately want to use objects which are only visible from one side. Backface cullling is a way we can do this
3. Sometimes due to limitations of buffers

### Backface Culling
If you're looking at the back of a face, that means that its **normal is facing away** from you. Aside from clever usages of this technique for effects, backface culling can discard vast swathes of your geometric world which don't need to be rendered.

Say you have a sphere: only the faces facing the camera (or those almost-facing-the-camera ones on the side) are going to be visible, the rest will be hidden (or **occluded** if you want to be fancy) by the front ones. We can make an assumption that faces pointing away from the camera are going to be occluded, and so discard from further rendering steps.

This works very well for enclosed meshes (like our sphere), but breaks down when meshes aren't closed (like the ability to look through a wall from the back which shows up in a lot of games). However, we probably don't care in those cases since the player is probably never meant to see that.

### Depth Culling
We do depth culling for two reasons. The first reason is performance: really far away objects probably don't need to be rendered, since they're tiny, or can be hidden with fog or clever level design. Likewise, very close objects are probably either inside or behind the camera, and so shouldn't be rendered.

However, there's actually another problem with rendering depth. The depth buffer, which stores the distance from the camera to the nearest thing in the world, has limited precision. After all, it's just a floating point number for each pixel on the screen, and `float`s have upper and precision limits. Floats can only measure increments of a certain precision (for 32-bit floats, that's about $1.17549\times10^{-38}$), and can only measure up to a certain value (for 32-bit floats, it's about $3.4028237\times10^{38}$). More importantly, the depth buffer is mapped between $0$ and $1$, meaning when the depth is equal to our far-clip-depth, we get $1$ and when it's equal to the near-clip-depth, we get $0$, and things rendering outside that range would break the $0..1$ logic. *And* the depth buffer gets less precise the further you are from the camera, so we need to limit how far away and how close things are allowed to be rendered to avoid artefacts.

So, we **cull** very far away objects because of precision problems and because those objects are probably too far to see clearly, we cull very close objects because they're probably inside the camera and because of precision problems, and we cull things behind the camera because they're obviously not going to be visible (remember that the depth value for a particular vertex might have a negative value, which means it's behind the camera).

### Frustrum Culling
We can also do what's called frustrum culling. If something (an object, a triangle) is completely outside the view of the camera (remember the frustrum from the projection section), then it'll be offscreen. If we can discover this quickly and easily, then we can cull even more geometry and optimise our game even more.

### The Drawbacks
So, **culling** is great, but it has some limitations. First, we're cutting corners. Maybe some objects will be see-through from behind. Maybe some objects will pop in and out of existence when far from the camera. Those might look silly or embarrassing in a cinematic game.

Secondly, and more importantly, the checks necessary to implement culling *also take time*. For instance, if checking to see if a triangle is onscreen takes 2 milliseconds, but rendering that triangle takes 10 milliseconds, that's going to add up over a lot of triangles. Unless that check saves us from rendering about 1 in 5 triangles, it isn't going to be worth having the check. This means we need to balance when we cull, and what we cull.
Frustrum culling is a bit complex and involves bounds checking (i.e. does the bounding box of this thing intersect the camera frustrum?), which can be time-consuming. Best to do it on bigger things, like entire objects. That way we only do one bounds check for perhaps tens of thousands of triangles (and we can even cache the object's bounds alongside its geometry to speed up even more. Yes you could technically do this with every single triangle but that means a *tonne* more data to cart around).
Backface culling is very easy to check with some multiplication and addition, and it's quite likely to exclude geometry (assuming it will discard 50% of the scene's geometry, that's a HUGE saving for such a cheap check), we can only really do it per-triangle, so we do this before we do any other math on a particular triangle.
Most of all, consider at what point in the pipline you're going to have the data at hand to decide whether or not to render something. If you have to do a bunch of maths to figure out if something should even be drawn, it might be a waste of time. If you're using values that already exist (like the normal of a triangle for backface culling), you're probably saving time. Overall, if you're building something like this, the best solution is to try it out, then profile it: *does solution X make it run faster?*
You get the picture.

### Aliasing
Aliasing is something that happens due to the granularity of the space we're working within. By granularity, we mean **pixels**. Things in the real world aren't perfectly square, or perfectly vertical or horizontal, which causes problems when you try and quantize that and squeeze it into a grid.
When you take a photo, each pixel is affected by a bunch of different light rays, so you get a natural blurring effect in camera, but when you're 3D-rendering something, you lose that, since the rendering process only samples discrete objects (i.e. one object per pixel). This leads to nasty, hard, crinkly edges on objects or triangles which look really ugly.

Enter, **anti-aliasing**. Anti-aliasing encompasses various methods to minimise aliasing, and they span a spectrum from super-fast to slow-but-looks-great.

The most basic of these is probably one you're already thinking of: just do more than one sample per pixel! For each pixel, instead of doing one sample through the 'middle' of that pixel, divide the pixel into 4 sub-pixels, and render each sub-pixel, then average the results together to get the value for the pixel as a whole. This sounds great, and looks great (in fact, the more samples and subdivision you do, the better it looks), but as you'd expect, can get horrendously slow (I mean, you're quadrupling the number of pixels you have to render, of course it's slow). There are clever ways to make it less horribly slow, like **MSAA** and **SSAA**, but the problem persists.

Another way of doing this is just to stick with the data you have and blur the whole image. If you do this to the entire image it obviously looks like you've just applied a blur filter over the image, but algorithms like **FXAA** and **MLAA** are clever enough to perform edge detection and only blur the image a small amount and in particular places to preserve edges while smoothing out hard lines. These algorithms are *very* cheap, but they aren't amazing and are subject to artefacts, and do make edges look a bit blurry in some cases.

Techniques like **SMAA** blend some of these two approaches together to get a better result, which makes them somewhere in between on both performance and quality. Generally speaking, you can come up with better or worse algorithms for doing anti-aliasing, but the more maths your algorithm has to do, the worse its performance will be. If you can get a lot of quality in limited maths, well done.

Kind of in a class of its own is **TAA**, which works kind of like multi-sampling, but by using data from previous frames to stand in for extra samples. This works great, and is cheap as hell, *but* breaks down quickly when you have significant motion on screen, or when fading between two completely different images.

Of course, all of these methods are implemented various different ways across different platforms, engines, hardware, etc.

### Where Does Aliasing Happen?
Well, pretty much any rendered buffer. Imagine you're looking at a particular object, like a teapot. In order to render it, you're casting a ray out through the center of each pixel on your screen, and each of those rays will either hit the teapot, or miss it. In reality, there are trillions of light rays hitting your retina, to the point that the edge of the object is defined extremely finely, and the transition from teapot to background is blurred by the sheer amount of data coming in, so that for an 'eye-pixel', we might find a 'the object is sorta visible' case. In a computer, we only know whether the middle of a pixel can see the teapot or not, locking us into the rigid alias-ridden grid that is the digital world.

This means aliasing happens in the depth buffer, colour buffer, pretty much anything in fact. It's inescapable! AAAAAAA-

# Shaders
Shaders are a useful way of conveying the maths we want to do on our scenes in order to render it. They're a way of encapsulating a block of code as data which can be passed around (most importantly passed to, and understood by, the GPU). A shader normally takes some parameters, and outputs a single value (a single float, a colour, etc).

The three types of shaders are
1. **Vertex shaders** - executed per-vertex, on every vertex in a mesh
2. **Fragment shaders** - aka pixel shaders, executed per pixel on every triangle on screen
3. **Compute shaders** - not directly relevant to this pipeline, a useful way of shifting computation onto the GPU

Vertex shaders are executed first in the pipeline. As input, they often access vertex position, current time, vertex colours, vertex normals, and so on. They may store new properties on the vertex, like calculating some new extra special value based on the position and time, and may overwrite data like normals, position, and colours.

Fragment shaders are executed after vertices are transformed into view space, and is where the real 'rendering' happens. Data stored on vertices (like normals, UVs, and so on) is **interpolated** (see above) across the triangle and the interpolated value for a particular pixel is passed into the fragment shader. Fragment shaders may sample **textures**, perform **lighting** calculations, and so on, and usually only output a colour, to be drawn to the screen buffer.

The key difference to keep in mind is that vertex shaders are computed per-vertex, and fragment shaders per-pixel. Data can be passed from one to the other.

> While it's not useful for this module, something that's worth understanding is that the power of shaders come from their ability to be executed in parallel. The GPU's strength in computation primarily comes from the fact that although its processor clock is slow, it has many, many shading cores available to work in parallel.
> GPUs execute shaders by spinning up all those different cores, and assigning each one a particular pixel or vertex to execute the shader on. Because of this scheduling, the GPU has to wait for all the pixels to finish calculating before it can assign a bunch more pixels/vertices to the cores to be calculated.
> This means that, when writing shaders, you need to try and ensure that all your shaders execute in similar time. That means being careful with loops because if a couple of pixels take 10x as long as the rest, you're going to waste a lot of GPU time while the scheduling system waits for those last pixels to finish before assigning more work, meanwhile most of the GPU cores are just idle.

# Buffers and Applying All This Stuff

# A Few Programming Concepts

# How Do I Do This in OpenGL?
**IMPORTANT NOTE: THIS STUFF ONLY APPLIES TO OPENGL 1.x; WHILE SOME OF IT MAY APPLY TO LATER VERSIONS, BE WARY WHEN RESEARCHING. MOST OF YOUR RESULTS WILL BE FOR NEWER VERSIONS WHICH MAY BEHAVE DIFFERENTLY OR HAVE FUNCTIONALITY WHICH DOESN'T EXIST IN 1.x. BE WARNED**
Explaining fully how to use OpenGL in detail is difficult, so I'm gonna start by just doing a bit of a summary of the functions you probably need to use and what they actually do. But first, a few things.

## What is OpenGL Doing?
OpenGL's job is twofold: handle the low-level rendering of triangles; and talk to the graphics card in order to get that done.
It's useful to remember this when you consider how OpenGL 1.x works. OpenGL is a **state machine**, which means that rather than just telling it to do things outright, you tell it what state to go into, and then provide it with some extra stuff which is handled depending on that state. That means that you need to be careful when writing code that you know exactly what state OpenGL is in at any given time. For instance, before you perform a transformation (like `glTranslate` or `glRotate`) consider whether you're using the `GL_MODELVIEW` matrix stack, or the `GL_PROJECTION` matrix stack.

## What The Hell is a Matrix Stack?
Since OpenGL is a state machine, one of its states is the current matrix, applied to vertices in order to transform them. Remember all the way back in the first two sections or so, we talked about **matrices**, the mathematical objects which can transform **vectors** between coordinate spaces? You may also remember that we can combine matrix transformations into a single matrix using matrix multiplication. This is very useful. Consider a hierarchical scene structure, like you have in Unity or Unreal or Godot or basically any other engine or 3D software: when _object a_ is a child of _object b_, _object a_ will inherit the transformations of _object b_ (i.e. if _object b_ is offset from the origin by $\begin{bmatrix} 1 \\ 3 \\ -4 \end{bmatrix}$, then all of its children will inherit that offset, plus their own individual offset).
Now, when we want to transform _object a_'s geometry from model space into world space, we'd have to apply the _object a_-to-_object b_ matrix, then apply the _object b_-to-world matrix (and then the other stuff, but don't worry about that for now).

Now, although OpenGL only lets us have one active matrix at a time, the stack allows us to save and store matrices which we can later revert back to. This is *super* useful for a hierarchical scene, since it means we can easily apply parent object transforms to child objects something like this:
1. Apply the transformations of the current object (position, rotation, scale)
2. Draw the current object
3. Push the current matrix down the stack
4. Recursively jump to step one, but for each child object
5. When done, pop the current matrix
This careful pushing and popping of matrices before applying transformations means that we can safely undo transformations so that transforms from one object don't affect transforms of another object (unless we want them to, in the case of child objects).

When we push to the stack, everything gets shifted down and an identical copy of the matrix that was on the top of the stack before is inserted at the new top. Conversely, when we pop the stack, the topmost matrix is discarded and everything is shifted up. **Transformations are always applied to the matrix at the top of the stack.**

## On Operation Ordering
Cast your mind back to the first two sections, where I explained that transformations are actually applied to vertices in the opposite order in which they are issued as commands (i.e. via `glTranslate` or `glRotate`). In matrix terms, a compound transformation looks something like this:
$$translation \times rotation \times other...$$
and every additional transformation is being multiplied onto the right hand side. However, when that transformation is applied to a vector, the vector is also on the right hand side, so the effective order to transformations is reversed:
$$translation \times (rotation \times (scale \times \begin{bmatrix} x \\ y \\ z \end{bmatrix}))$$
and we end up doing the scale first, then the rotation, then the translation. In practice all of this is combined into a single matrix but this ordering remains the same.

## Actually There Are Two Stacks
As you've noticed, OpenGL actually has *two* matrix stacks: the **modelview** stack and the **projection** stack. These are pretty much what they sound like: two separate stacks, one of which you should use for model-to-view transformation (i.e. the position/rotation/scale of your camera, objects), moving from object-local space into world space, and then into camera space (see the earlier section on projection for more info); the other of which you should use for the projection transform whether perspective or orthographic, or some hideous abomination of something else.
OpenGL does this so that you can separate the two and just make your life easier. Remember that transformations are applied in the opposite order to that in which they are given, so since the projection transform must happen last, it must be inserted first. If you wanted to change your perspective transform mid-frame, you'd need to pop all the way down the stack in order to get at the projection matrix, and then reapply all your other transforms again. Separating the two also helps prevent you fucking up the stack in some horrible Lovecraftian fashion.

## The OpenGL Cheatsheet
// TODO: big ol todo here
Ok I hope I get all of this right. I won't cover every variation of every function here, just enough to give a solid overview of what different things are doing. A few definitions:
Currently active matrix - the topmost matrix in whichever matrix stack is currently active
Identity matrix - a matrix which represents 'no transformation'

### Matrices and Transformations
Remember that these commands **don't directly transform the geometry**, they transform the **matrix** which is **then applied to the geometry** in order to transform it.

`glTranslatef(float x, float y, float z)` - translate/offset the currently active matrix by a given direction vector
`glRotatef(float angle, float axis_x, float axis_y, float axis_z)` - rotate the currently active matrix around the axis (i.e. direction vector) described by the last three arguments, by the specified angle
`glScalef(float x, float y, float z)` - stretch/scale the currently active matrix by given amounts in each axis
`glPushMatrix()` - pushes the currently active matrix stack down by one (see above), leaving a copy of the previously active matrix at the top
`glPopMatrix()` - pops the top of the currently active matrix stack, removing whatever is currently at the top and shifting everything else up by one to replace it
`glMatrixMode(/* either GL_MODELVIEW or GL_PROJECTION */)` - switches the currently active stack to whichever is specified, so that all subsequent transformations are applied to the top of the specified stack
`glLoadIdentity()` - replaces the currently active matrix with the identity matrix, equivalent to resetting the transformation
`gluLookAt`
`gluPerspective`
`gluOrtho`
`glViewport`
### Drawing Geometry
`glBegin()`
`glEnd()`
`glDrawElements`
`glEnableClientState`
`glDisableClientState`
`glVertexPointer`
`glColorPointer`
`glNormalPointer`
`glTexCoordPointer`
`glVertex3f`
`glNormal3f`
`glColor3f`
`glTexCoord2f`
### Textures
`glGenTextures(int how_many, int* where_to_put_the_ids)`
`glBindTexture(/* for these purposes, should always be GL_TEXTURE_2D */, int texture_id)`
`glTexImage2D(/* for these purposes, should always be GL_TEXTURE_2D */, ... TODO`
`glTexParameterf`
### Lighting

### Initialisation
`glEnable`
`glDisable`
`glClearColor`
`glClear`
`glFlush`
`glCullFace`

projection
textures and texture coordinates (minifcation, magnification, mipmapping and filtering)
GL architecutre/pipeline
 AAAAAAA