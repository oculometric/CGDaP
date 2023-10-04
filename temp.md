# Portfolio

Briefly, I have various skills as an artist in digital 3D, as well as traditional drawing skills. I can develop and understand programs in C#, C++, python, and GLSL, among others. I have experience predominantly in **Blender, GIMP, Unity, Unreal Engine**. I'm currently studying games design and programming at Staffordshire University.

My 3D skills include **modelling** (mostly hard-surface and foliage), **texturing** (procedural, hand-painted, and mapping pre-existing textures), **UV unwrapping**, **lighting**, and **compositing**, all of which I developed in **Blender**. Additionally, I have solid **drawing skills, useful for prototyping ideas** and planning scenes before moving them into 3D.

My programming skills lie mostly in **C++, C#, and python**, but I have experience with various languages and environments including **GLSL and HLSL**, Java, Assembly, C, and GDScript. I'm also proficient with understanding **node-graph-based scripting and shading languages**, having experience with Unity's shader graph, Unreal's Blueprints and material graph, and Blender's material and geometry nodes.

[![B8ce50432720755aadfd9cbb5cd32710](https://cdnb.artstation.com/p/content_assets/assets/000/172/317/original/b8ce50432720755aadfd9cbb5cd32710.png?1696416205)](https://cdnb.artstation.com/p/content_assets/assets/000/172/317/original/b8ce50432720755aadfd9cbb5cd32710.png?1696416205)

"A Lonely Greenhouse" - above is a short hidden-object **puzzle game made with Unity**, with a focus on a distinctive art style. This project taught me a lot about Unity, as I ended up making use of a range of features, including the Input System, animation utilities, C# API, post-processing with the URP, physics, and particle systems. In particular, learning to use **animation controllers** to switch between animation states I found interesting, which I used for the plant cutters to create a 'snip' animation when you use them to cut ivy.

The art and **assets for the game I did in a pixel-art style in Blender**. This afforded me a lot of practice not only with modelling various elements (the greenhouse parts I particularly enjoyed, I made them as a kit which can be freely assembled, though I didn't end up using many parts of the kit), but with **pixel-perfect UV unwrapping** (for which I wrote a python script to help) and painting or **touching-up textures by hand**.

I was also quite proud of the **procedural ivy growth algorithm** I wrote, which I built as an editor tool for Unity. It works by projecting new branches against scene physics geometry, using various weighted vectors (previous growth direction, surface adhesion) to determine where it will grow next, and ensuring it doesn't intersect with objects in the scene.

This project was also a learning experience in terms of **responding to user feedback**: several friends were happy to playtest for me, and talking to them to figure out what needed to be improved or changed to improve the user experience (for instance, adding hints/descriptions at the bottom of the screen, and changing the speed at which objects snap to the cursor when held) helped me to **practice communication and understanding user needs based on feedback**.

Everything in this project, besides some of the sound effects and the Unity Player were created by me.

[SEE THE PROJECT IN DETAIL HERE](https://oculometric.artstation.com/projects/1xYBqK)

[![463922903bd49b514509cff531275972](https://cdna.artstation.com/p/content_assets/assets/000/172/318/original/463922903bd49b514509cff531275972.png?1696418131)](https://cdna.artstation.com/p/content_assets/assets/000/172/318/original/463922903bd49b514509cff531275972.png?1696418131)

"Untitled Stairway II" - above is an exercise in **visual storytelling**, following a 4-panel comic style. This is all made entirely within **Blender**, save for combining the four panels at the end (done in GIMP). I developed the graphite art style over the course of previous projects, and it consists of materials with special AOV passthrough properties, careful lighting, and a **complex compositing setup** that takes into account rendered colour, normals, ambient occlusion, and the AOV passthrough to produce the final output.

I challenged myself with this project to experiment with ways different elements might decay: the cardboard box the TV is sitting on crumples; the orrery gets broken; tiles get dislodged; meanwhile ivy, grass, and the spider-plant thrive. I made use of **shape keys/blend shapes** for the spider-plant, tiles, and cardboard box.

The ivy is **procedurally grown using a script I wrote in python for Blender** (in fact, the Unity script mentioned above is based heavily on this script), and I then used **geometry nodes** and **keyframe animation** across 4 frames to make it look as if the ivy grows over time.

Mostly this project was practice turning a simple starting scene into a complex, 'well-used' feeling endpoint, by **iterating on the scene** and concept.

[SEE THE PROJECT IN DETAIL HERE](https://oculometric.artstation.com/projects/49eR5l)

[![C2e5218b2ecc1ffad9c488c1d2aa578e](https://cdnb.artstation.com/p/content_assets/assets/000/172/319/original/c2e5218b2ecc1ffad9c488c1d2aa578e.png?1696419683)](https://cdnb.artstation.com/p/content_assets/assets/000/172/319/original/c2e5218b2ecc1ffad9c488c1d2aa578e.png?1696419683)

[![0266085232923eecf27963625ec1cc89](https://cdna.artstation.com/p/content_assets/assets/000/172/320/original/0266085232923eecf27963625ec1cc89.png?1696420623)](https://cdna.artstation.com/p/content_assets/assets/000/172/320/original/0266085232923eecf27963625ec1cc89.png?1696420623)

"pipe grotto" - above is a project focussing on two main things: dramatic, **bold lighting**, and conveying a slightly unsettling, **uncanny atmosphere**. This piece grew from a drawing exercise I did as part of a drawing foundation course I took, during a module on tone. This project allowed me to apply **practice in designing scenes** as well as show off **dramatic tonal range** in Blender. I wanted the space to feel empty, but not entirely empty, hence the sparse details mostly toward the edge of the frame, such as the chair, wooden debris, and cloud.

As you can see in the second image above, I developed **my own compositing-based dithering algorithm**, to produce a pixel-art-esque effect and to contribute to the overall atmosphere, as the piece relates to the analog horror genre. This works by rounding the colour of each pixel (using HSV rather than RGB to give more control) to the nearest step, then using the difference between that step and the pixel's real colour to pick a dithering pattern between the lower bound step and the higher bound step (i.e. if the pixel's colour is halfway between the steps above and below it, then a checkerboard pattern will be used, which has half-and-half of the upper and lower steps), which over an area of similar pixel colours, produces a nice dithering effect. I've since **re-written this dithering algorithm as a GLSL shader** for use with game engine projects.

[SEE THE PROJECT IN DETAIL HERE](https://oculometric.artstation.com/projects/8b1PER)

[![Ec0433d7ac6adc5e3c9d2c568d91557a](https://cdnb.artstation.com/p/content_assets/assets/000/172/321/original/ec0433d7ac6adc5e3c9d2c568d91557a.jpg?1696421256)](https://cdnb.artstation.com/p/content_assets/assets/000/172/321/original/ec0433d7ac6adc5e3c9d2c568d91557a.jpg?1696421256)

"RETURN" - above is a project I did as my submission to the **Atomhawk Design contest** 2021, the theme being 'the return'. As such, I envisioned a story about someone coming back to a place long-forgotten, at the center of a hedge-maze. This meant making clear the time difference between the protagonist's first visit and their return, hence the damage to the central tower, overgrown ivy and long grass, in order to **implicitly tell a story**. I was inspired partly by the towers at Hampton Court Palace for their odd picturesque-ness. I even wrote a short story to go with the piece, which you can read on the dedicated page (it also contains WIPs, alternate views, and more).

The main challenge of this project was making the tower and space look as **messy and abandoned as possible, while also managing scene geometry** to stay within my system resources. I manually cleaned up ivy (for this project, generated with Blender's built-in ivy generator) to maintain its visual density while significantly reducing its vertex count, a **skill I've since further developed** having moved more into game work.

This project also makes use of an **artistic sky and lighting setup**: the sources lighting the scene are completely different from the visual sky, which was composited in at the end.

[SEE THE PROJECT IN DETAIL HERE](https://oculometric.artstation.com/projects/J9mQAD)