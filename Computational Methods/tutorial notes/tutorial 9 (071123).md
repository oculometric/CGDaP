- start by defining the adjacency matrix and precalculating a matrix of taking different weights between different planets
- format table as 5 different tables, each for a different starting planet
- columns represent the next planet visited
- rows represent the current configuration. do it in blocks (same table) where the first vertical block is just the start planet (e.g. A), the second is AB AC AD AE, then compound to three planets, etc
- only carry forward to the next block the best scenario for each set of planets (i.e.  each permutation)
- repeat until we've reached a total of 5 planets, and pick the best route that starts at A  
- repeat all of that again from a different starting point
- **DYNAMIC PROGRAMMING BUILDS UP SOLUTIONS FROM PREVIOUS ANSWERS**

