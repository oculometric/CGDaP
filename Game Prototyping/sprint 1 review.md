during my first sprint i worked Wednesday - Sunday (inclusive). here's all the tasks i got done:
![[Pasted image 20240318102735.png]]
![[Pasted image 20240318102752.png]]
in case you didn't read the first post, the numbers in brackets indicate: {effort_value, time_estimate > actual_time}.

first of all, my time estimates. most of them were reasonably accurate. i broke my work down into lots of small tasks, which meant most of them were small, 30-minute blocks. a lot of my shorter estimates were a bit above the reality, but then a few i significantly underestimated. overall, excluding time spent managing (i.e. source control, task management, forum posts), i spent just over 8 hours on tasks that i estimated would take me a bit under 7 hours, over the course of five days (although i didn't work on the project every day, due to lectures and having work from the other module).

i actually didn't find my 'effort values' all that useful. i mostly just worked on tasks in the order that they were appropriate to work on.

## problems i faced
one major challenge i faced during this first sprint, was how to break up my game-grid handling code. as much as possible i wanted to **encapsulate** the behaviour of managing the tile grid into a single script, and to hide the underlying data structure of the grid. the structure that i settled on to make code as clean as possible was the following structure:

Tile Manager - behaviour on the Tilemap object which handles the tile grid data structure, and talks to the different tilemap layers to update the tilemaps accordingly
Game Controller - singleton which sits on an empty object and get references to the player, tile manager, core, and generator on start, and handles the 'game rules' (i.e. iterating the game each time the player takes a turn)
Turn Handlers - behaviours which exist on any entity that wants to have a place in the grid, which encapsulate functionality for trying to perform the different actions in the game (move, activate tile, destroy link, create link) and talk to the game controller

screenshots of this stuff

this allows me to implement all the checking behaviour (things like 'is the entity attempting to move outside the grid?' or 'can the entity create a link between these two tiles') in the turn handler, which then calls the function on the tile manager to manipulate the underlying tile data to actually do an action (create a link, etc). thus any entity which i want to be able to act, just needs to implement behaviour for deciding what move to make, and then call into the relevant method in its copy of the turn handler behaviour (minimising **code duplication**).


a more minor challenge i faced was creating the sprites for my tile grid. this actually came as multiple challenges. i realised when making my simple sprites that the 4 types of tile (with 4 different actions) multiplied by 2^8 link configurations, multiplied by ~6 different cooldown states would result in *a lot* of tiles. to solve this i split my sprites into layers: a base layer (the 4 action sprite types), a cooldown overlay (the 6 different cooldown states), and two layers for the different link types A and B (each with 2^4 link states, each of the four cardinal directions either being linked or not linked). this was much more manageable to update and display.
this did introduce a slight other problem, which was how exactly to display the cooldown. i wanted the underneath tile to still be visible, so i went ahead and created a simple **shader** using the shadergraph which blended the tile sprites **multiplicatively**, giving a nice dimming effect over tiles, with a numerical cooldown value.
these two together actually did increase the time i took to complete the sprint somewhat and i added the 'tile link sprites' task midway through the sprint to account for the extra work which became required.

image of the different sprites/layers, screenshot of shader graph

this is something i was **taking into account** when i planned the sprint: i intentionally tried to over-estimate somewhat and i tried not to load too much stuff onto a single sprint, since i know from experience that there's a tendency for other tasks or required fixing-of-things to come into focus after you start working on a system.


overall i'm very pleased with what i've got done in my first sprint. i've built the turn-taking system, the control of the game board (the tile grid), and i've laid the foundations for building other behaviours on top to use this system, such as enemies. a **burndown chart** based on my performance data from this sprint is below.

i also found myself adding tasks to my list of overall things-to-be-done (i.e. not assigned to a particular sprint yet), for instance i need to design a level/levels or come up with a system for generating them procedurally.

## performance in detail
![[Pasted image 20240318130151.png]]
work remaining represents the 'predicted time' as tasks are completed, while time spent is the actual amount of time i spent working on tasks.

almost all of my work happened in the afternoon, **between 12:00 and 16:00**, although this likely isn't very useful since my schedule is primarily dictated by when my lectures are.

my session length ranged **between 50 minutes and 2 hours**, which seems fitting as i tend to work for quite a while once i get started on something.

i found that having concrete goals, particularly having goals that were well-broken-down into manageable tasks helped me keep track of what i needed to be doing as well as not feeling overwhelmed by things.

## sprint 2
for my second sprint, i'll probably also try to stick to a 5-day schedule, since that worked quite well (and i do have another module to push on too) and it gives me time to reflect in detail. here are the tasks i've assigned myself in Trello for my second sprint:
![[Pasted image 20240318120207.png]]
this totals 5.5 hours of work, but i'm anticipating that some of these might end up taking more time than expected (then again, that could be wrong, and i may re-scope and assign more tasks mid-sprint if that seems reasonable).
the groundwork i did in the last sprint should help a lot with making these tasks manageable.