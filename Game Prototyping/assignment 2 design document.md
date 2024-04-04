## summary - "Plant Watering Simulator"
the game will encompass the player exploring a semi-procedural 3D world in order to water plants scattered around the world. the player's view of the world at any one time is limited.

## setting, theme, style
the game will be set initially within an **office**, which the gameplay draws the user out of and into a **garden/allotment** setting which makes up the majority of the game.

>*the user initially takes a break from their work to water their desk plant, but in doing so discovers other office plants which need watering, and exploration of the world unfolds from here.*

various types of **subtropical plants** will be featured, in typical 'low-key' **garden pots and planters**. in order to add detail to the world and limit the player's movement, elements like brick walls, fences, raised walkways, etc will be present.

the game will be styled with **pixel-art** textures and objects block-ified to the pixel grid. it feature a somewhat **saturated colour** palette and a **dusty, slightly overgrown** overall look. it should have a generally **relaxed** feel, which can be influenced by specific sound design, rendering, and animation/camera control choices.

## game loop, goals, challenges
```
flowchart TD
    A(Discover plants which need watering)
    A --> B(Search for water source)
    B --> D(Look for closer water source)
    D --> C
    B --> C(Return and water plant)
    C --> E(New chunks become visible)
    E --> A
```
![[Pasted image 20240402154945.png]]
the user is asked to water plants, which they can do by bringing water from water sources, in containers, to plants which need watering.

>*the user is challenged by continuously extending the play space and encouraging the user to learn the layout of the space in order to more efficiently complete the objective (watering plants)*

new water sources might be found, as the map is explored to minimise the time spent going back and forth between plants and water sources.

>*the user's overall goal is to water all the plants in the map. the map has a limited overall size and this objective can only be completed when the whole map has been explored and all plants discovered*

the game should keep a counter of how many plants the player has discovered and how many they have watered, although as they continue to explore the map, the 'discovered plants' counter will continue to be ahead of the 'watered plants' counter.

>*the user is rewarded upon watering all plants on the map by being called back to the office to continue their work*

there is no real 'lose condition', the game simply continues until the 'win condition' (watering all plants in the map) is met, though the game should also **keep track of how long the user has taken** to complete the objective.

>*when the user has watered all plants, and subsequently returned to the office, the game will end*

## core mechanics
### segmenting the world and limiting visibility
the game world is viewed from an isometric 3rd person perspective. the player character is centered in the view at all times. the world is segmented into chunks, square vertical blocks, which may be visible or invisible at any particular time. to encourage the player to learn the layout of the world, only a 3x3 array of chunks are shown to the player at a time, and this 3x3 array is centered on the player. these chunks are swapped in and out as the player moves through the world:
![[assignment_2_movement.excalidraw]]

### watering plants
the game world is filled with plants, which conceptually are objects which register as being 'watered' when their 'water meter' is filled. different species of plants may have different watering requirements. a visual change should be displayed when a plant's water requirements are met. plants which still need water should also be indicated visually, potentially with a non-diegetic overlay.
![[assignment_2_watering.excalidraw]]
when watering plants, the water in the source is consumed. different water sources may be better or worse than others:
- initially the player only has a small cup -> very low volume
- the player soon discovers watering cans -> better volume, but still limited
- some areas may have hoses -> infinite water, but limited radius of usage
- further into the map, the player can find higher volume watering cans -> large volume
watering cans may be refilled from water sources such as taps or fountains.
the limited carrying volume of watering cans encourages the user to search for water sources close to the plants they are trying to water.

### procedural map generation
the map generation of the game should be procedural/semi-random, which will create variety. generation will based on the wave function collapse algorithm.
```
flowchart TD
    AA[Generate Map]
    AA --> A(Decide map size, seed)
    A --> B(Insert initial chunk patterns)
    B --> C(Pick the chunk with the fewest\n possible pattern options)
    C --> D(Randomly decide a \npattern for the chunk based\n on the surrounding chunks)
    D --> E{Have all \nchunks been given \npatterns?}
    E --> |yes|F[Map is complete]
    E --> |no|C
```
![[Pasted image 20240404124429.png]]
plants will be placed randomly within each chunk, based on the same seed. a flood filling algorithm will ensure that plants are always placed somewhere that is accessible to the player.
hoses and taps will also be placed randomly within the map, but in a way that guarantees a minimum and maximum distance from one another.

### blocked off areas
// TODO:

## inspiration
Cloud Gardens - for its relaxed style and pastel, pixel-art art style
![[Pasted image 20240404125440.png]]
Power Washing Simulator - for its use of water to alter the environment in order to achieve an objective
![[Pasted image 20240404125904.png]]
Slime Rancher - for its forcing the user to carry water they need from a source, rather than just having it on tap wherever they are (like in PWS)
![[Pasted image 20240404131356.png]]
