for this sprint i worked Monday and Tuesday. having just finished, this is the state of my Kanban board:
![[Pasted image 20240319121848.png]]
although i adjusted some estimates, these ones were way more off from reality compared to last time. i think this is mostly due to the strong foundation i set up in the last sprint, making these tasks much easier and less complicated than expected. this sprint being so much shorter, i can't really meaningfully comment on the time i spent on it (see performance review below), but in summary, i spent **3 hours** on tasks i predicted to take **just over 5 hours**.

i found myself adding a task, specifically to realise the player and enemy positions in game (i.e. turn their grid positions into proper transform positions), which was easy.
## problems i faced
i actually faced quite a significant problem during this sprint: when implementing the checking behaviour to test if there is a route between the core and the generator, i found that i couldn't use `Vector2Int` with the `SortedSet` type, due to it not having comparison behaviour.
![[Screenshot 2024-03-18 211620.png]]
i solved this (with the help of Stack Overflow) by implementing a custom comparer class and initialising the `SortedSet` with it. after some testing, i successfully got the condition checking working.

!!video of stuff working!!
## performance in detail
![[Pasted image 20240319123631.png]]
again this sprint, having concrete, small goals to complete helped make the work manageable and keep me focused. however with sprints being so short, i end up spending a lot more time just reviewing compared to my first, longer, sprint.
## planning sprint 3
i finished with a reasonable amount of time left over this sprint, and while i don't have time to move more tasks onto this sprint, i think i can be more ambitious on the next sprint. on top of this, i think it's reasonable to (tentatively) **increase the scope** of the project. i did end up adding a few tasks to the project overall during this sprint, including remaking the tiles and sprites to be double the resolution (they're too small to be properly legible), adding instructions, and adding sound and visual effects. as such, my Kanban board for the next sprint looks like this:
![[Pasted image 20240319124545.png]]
