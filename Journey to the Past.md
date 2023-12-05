# Journey to the Past

Dorling Kindersley's _Eyewitness Virtual Reality Dinosaur Hunter_ is a 1996 edutainment product. It was distributed as a CD-ROM for Windows 95, and MacOS.

## Subject Matter and Presentation

_Dinosaur Hunter_ is presented (as the title would suggest) as a virtual museum about dinosaurs, which the player can walk around and explore semi-freely. It covers a range of time periods (Triassic, Jurassic, and Cretaceous) throughout the reign of the dinosaurs, including examples of dinosaurs from those time periods. These come in the form of large exhibits, maps and models, labelled diagrams, and interactive dinosaurs which are reconstructed by the player and then will proceed to wander around the museum.

## The Museum

The setting of _Dinosaur Hunter_ is a museum in the shape of the Eyewitness logo, consisting of a large circular *arena* in the center, two trapezoidal *wings* on either side, and corridors encircling and separating all three.
The museum appears to be constructed out of ancient reddish-brown stone, almost brick-like in appearance, with gritstone pillars, while the floor is sandy. Lighting is provided by floor-mounted spotlights, as well as many invisible downlights and area lights.

In the *arena* is the main exhibit, a Tyrannosaurus and a Triceratops. Around them spiral two sets of staircases, which meet on the bottom level and end in dead end viewing platforms on the top level. The ceiling is arched toward the centre.

The *west wing* contains the *dinosaur excavation site*, the game's main attraction. It consists of an elevator accessed by suspended gantries and a strange device which cannot be reached. In here the player can descend from the museum on the elevator to three different levels of rocky excavation. Scattered around these are bones from different dinosaurs, which can be scanned to determine their age (and thus what dinosaur species they are most likely from) and placed into labelled bins. Upon returning to the museum level, players are able to add the missing bones which they have collected from the subterranean levels to a set of six dinosaur skeletons. When done correctly the dinosaur in question will be brought to life by the strange device, and can be seen running out of the west door of the _dinosaur excavation site_ room, subsequently roaming the museum.

The _east wing_ contains the _world of dinosaurs_, a room filled mostly with maps detailing the shapes of continents and how they changed during the period of the dinosaurs, where dinosaur fossils have been found, and more.

The _perimeter corridor_ which wraps around the entire museum and shows a timeline of dinosaur species from the Triassic (Coelophysis, Lufengosaurus, Anchisaurus), through the Jurassic (Allosaurus, Archaeopteryx, Stegosaurus), to the Cretaceous (Deinonychus, Giganotosaurus, Velociraptor).

There are also _dividing corridors_ which separate the _wings_ from the _arena_. East is _extinction theories_, _survival of the fittest_, _fossilisation_, and _sizing up dinosaurs_, while west is _evolution trail_, _dinosaur puzzle_, _identifying dinosaurs_, and _evolution spiral_.

The _southern corridor_ also gives access to the _store_ and _exit_, as well as _dino online_, _tours_ and the _index_.

## Rendering

Although the rendering quality is limited, not hyper-realistic by any means, the imagery has detailed and clear shadows from multiple light sources. This leads me to believe it is a display of ray-traced rendering. Another clue to this is that in animated cutscenes, we can see variable noise patterns fluctuating in the otherwise static background, which are tell-tale of a limited number of samples used during rendering. However there do not appear to be any reflections, suggesting a very simple path-tracer, if such an algorithm was used. The question of how such an algorithm would be able to run on home computers in 1996 is that it did not: the entire game is pre-rendered, and consists of many images which are transitioned between, stitched, overlaid as needed as the player navigates around the game. This highlights how especially impressive the number of animated elements are. Looking carefully at some of these, we can see that the background around the moving element subtly changes (due to rendering artefacts/noise) in a square area, exposing some of the clever methods used.
To move the user between images then, three techniques are mainly used. Firstly spontaneous cut transitions, where one images is just swapped in for the other. Secondly, fade transitions, implemented as individual pixels switching from one image to the other in a noise pattern. Thirdly, push transitions (mostly used when panning the camera) where one image is pushed offscreen by another, in the appropriate direction for where the views appear relative to one another.
These images are stored in only 8-bit colour and are heavily dithered, but this serves mostly to heighten the atmosphere and to hide many rendering noise artefacts.

_Dinosaur Hunter_ clearly makes use of repeating patterned textures, for the various types of stone, though the sand is too fine to see clearly. In at least one place, a clear musgrave noise pattern emerges. The game also makes use of normal/bump maps to convey the bumpy surface of rock columns.
The sand appears to use a procedural noise texture of some kind to produce a normal map on its surface.

Fog














# Building a New Renderer

Questions:
- should next event estimation be used?

Questions which are answered:
- A path tracing algorithm should be used
- The algorithm should support having a sky background light and sun lamp
- The algorithm should use a colour transform like AgX or Filmic
- The algorithm should use backwards path tracing
- Material transmission, subsurface refraction will not be implemented
- Materials will be handled either as purely Lambertian or purely specular, Lambertian materials will be randomly (roulette) sampled
- A bounding volume hierarchy, or potentially a Binary Space Partitioning method should be used to accelerate geometry searching
- Geometry should be divided into objects, each of which store their geometry as a set of lists (vertices (n) vector3, triangles (n) 16bit, normals (n/3) vector3, material (n/3) 8bit, uv (n) vector2, actual materials, plus lists for predefined variables of tris), and have bounds calculated to accelerate geometry searching
- Variable sampling depth should be implemented, but such as to avoid recursion, using only loops
- Many-lights should be implemented as material emission
- Lambertian materials should be sampled multiple times within a single surface bounce (i.e. multiple rays are cast out from a single Lambertian collision) to minimise resulting noise
- Multiple sampling should be implemented
- The algorithm should output depth, normal buffers as well as colour
- Floating point (32bit) values should be used to handle colour
- SSE is allowed, but data copying should still be minimised as much possible

TAKE A LOOK AT MAC3D