in this turn-based single-player game, the player's goal is to eliminate all 'enemy' entities from a grid of tiles. they do this by moving between tiles, interacting with those tiles, and making or breaking links between tiles, to either exclude enemies from the rest of the grid by cutting them off, or by destroying them using tile abilities.

input actions:
joystick + button -> attempt to move to tile in the direction the joystick is pointing
button -> trigger tile ability
button + button + joystick -> create a link between the current tile and the tile pointed to by the joystick
button held + joystick -> destroy a link between the current tile and the tile pointed to by the joystick

game rules:
- the player may only move between tiles along established links, which have the same filter as the player's mode (if the player is in mode A, they cannot move along filter B links), and may not move into tiles occupied by other entities (enemies, 'core', 'generator')
- the player can create links to cardinally adjacent nodes, but only once every 3 turns, only if a link does not already exist between the targeted and current nodes
- the player can destroy links to cardinally adjacent nodes, but only once every other turn, and only if the targeted node has a link to the current node
- every time the player moves or otherwise acts, each enemy will also get a turn, during which they may move or act
- the player will lose if they become unable to move into an adjacent tile, or if the 'generator' and 'core' are no longer connected by linked tiles
- the player will win when either there are no enemies left or all enemies are trapped within a single tile
- different tiles may have different special abilities:
	- destroy enemies on adjacent tiles
	- rotate links around clockwise (i.e. top link replaced with left, right with top, etc)
	- teleport player to opposite side of the board
	- switch the player's mode (A->B, B->A)
	
![[Pasted image 20240312115945.png]]

requirements:
- input handling system (state-machine?)
- conceptual grid-link handling system
- gameplay mechanism (i.e. interacting with that underlying grid), making/breaking links, moving, checking G-C connection, checking for player isolation, enemy isolation, etc
- updating display of player, grid, enemies
- enemy AI

basic sprint planning (will be revised to fit how exactly smaller subtasks end up going):  
sprint 1 : input handling, overarching grid-manager system with tilemap for display
sprint 2 : actual gameplay mechanism and rest of the display elements (player, enemies)  
sprint 3 : enemy AI and polish, and all the other tasks i end up needing more time for