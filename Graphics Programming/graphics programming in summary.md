
# Coordinate Systems and 3D Space
A coordinate system is just a way of representing transformations in a particular coordinate space. That might seem like a circular definition, but roll with it for a minute. This section covers important stuff about what vectors and matrices are, how they interact, and how those mathematical building blocks are combined to implement the 3D world in games. Brace yourself for a detour into matrices.

In our 3D, we represent our dimensions as the sum of three different axis vectors, the $X$ axis, $Y$ axis, and $Z$ axis. By default these have the values:
$$X = \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix}, Y = \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix}, Z = \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix}$$
This might seem redundant but it is a useful concept.
Thus we define a point in 3D space as having X, Y, and Z components. Let's define a point $p=\begin{bmatrix} 1 \\ 4 \\ 3 \end{bmatrix}$. We can say for this that $p = 1X + 4Y + 3Z$, where $X$, $Y$, and $Z$ are our axis vectors.

### Vectors
The follow-up question to this is *"what is a vector?"*. Conceptually, **a vector is a line between two points**, and is represented by the distance between those points as specified by individual $XYZ$ components (i.e. it has direction and magnitude, ayyyy). So a vector has the same structure as a point: three numbers, one for each axis. Conversely, we can also say that **a point is really just a vector which starts at the origin** (and ends at the point). This gives a bit more context to the idea that a point is represented by a sum of the three axis vectors.

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
In a previous paragraph we said that a point is conceptually a vector which starts at the origin. Well, *what happens if we move the origin?* If we do that, then we're effectively creating our own **coordinate space**. All our points are still measured from the origin, and described by a set of three axis vectors, so if we change the definition of the coordinate space by moving, rotating, or scaling that origin, **the same set of transformations are applied to the points defined within that space**.

Here is as good a place as any to emphasise that all coordinate systems are relative. For instance, it doesn't actually matter which axis you treat as the 'up' axis, whether it's $Z$, $Y$, or even $X$, *as long as you're consistent within your software, it doesn't matter*. I don't wish to make this existential but coordinate systems are really just a useful concept for concretising an abstract non-existent space with numbers, and as long as you handle those numbers, you can kinda do whatever you want.

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

# Geometry (dun dun duuuun)
In this section I'm going to talk about geometry in the narrow, triangle-mesh sense. However, there are other ways geometry can be expressed, lots of ways in fact, but they require cleverer algorithms and aren't what we're focussing on with this module.

A **triangle mesh** is composed of **triangles**, that's obvious. *Why?* Because triangles are the simplest 3D shape, they are guaranteed to be flat (think of a chair with three legs: there's no way to have one leg too short!), and doing maths with them is easy.

**Triangles** are bounded by **edges** which are composed of **vertices**. A triangle having three corners means it has three vertices.

When storing a triangle mesh, the first way to think about it is as a list of triangles, each of which contains three points, each of which contains three coordinates (so 9 numbers in total). However, the vast majority of those points are going to be shared between two or more triangles, so it makes much more sense to store the vertices elsewhere. Thus version two of our data storage consists of two lists:
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

# Lighting

# Aliasing and Culling

# How Do I Do This in OpenGL?

projection
interpolation
textures and texture coordinates (minifcation, magnification, mipmapping and filtering)
aliasing
GL architecutre/pipeline
 AAAAAAA