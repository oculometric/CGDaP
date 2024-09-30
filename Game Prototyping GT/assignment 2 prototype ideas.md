player moves in 'open world' between block tiles. only a 3x3 area is visible at a time, when the player moves into one of the tiles to the side, relevant tiles pop up or disappear.

player's task is to walk around doing something (watering plants? picking stuff up?).
watering plants:[[assignment 2 design document]]
- the player needs to fill up a watering can, requires knowing where taps are
- as they explore further from the start, they'll want to find more taps/water sources, so these should be dotted around
- endless? if the map is procedural the player can keep exploring further and further to water more plants. the game should keep a counter of how many plants have been watered vs how many have been seen (i.e. you enter a new chunk, 3 more chunks get loaded on the side, they probably contain plants that need watering, so the 'seen plants' counter goes up, when those plants have been watered, the 'watered plants' counter goes up, but by entering those 3 new chunks the player has likely encountered even more plants that need watering)
- maybe a hose? localised to a certain area but doesn't require going back
- if it was to work like this, could start in an office building, where you first start to get water to water your desk plant, which becomes watering office plants, and then leads you out to the wasteland/garden (surreal transition?)

movement/map principle
![[assignment_2_movement.excalidraw]]
pixel-arty style (0.02m texels).

map generation:
combination of noise texture, random value seeded per cell, wave function collapse. fixed map size/upper limit?