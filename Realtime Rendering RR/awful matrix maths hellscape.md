### in maths land
for **row major** ordering:
- vector is on the LEFT of multiplication
- i.e. $v'=v \cdot M$ 
- i.e. $$\begin{bmatrix}x' & y' & z' & w'\end{bmatrix} = \begin{bmatrix}x & y & z & w\end{bmatrix}\cdot \begin{bmatrix}00 & 01 & 02 & 03 \\ 10 & 11 & 12 & 13 \\ 20 & 21 & 22 & 23 \\ 30 & 31 & 32 & 33\end{bmatrix}$$
- translation is along the bottom of the matrix
- best way to remember this is that the MAJOR part is the VECTOR and it's in a ROW
- basis vectors (x, y, z, w vectors) are *rows*

other way round for **column major**. basis vectors are *columns*, vectors are columns, etc.

### in computer science land
HLSL and GLSL store elements in a column-major way. however, this is SEPARATE from column-major in maths sense, instead it means that in memory, elements are stored:
$$\begin{bmatrix}0 & 4 & 8 & 12 \\ 1 & 5 & 9 & 13 \\ 2 & 6 & 10 & 14 \\ 3 & 7 & 11 & 15\end{bmatrix}$$
however, HLSL when initialised, initialises in a row-major way (i.e. 0,1,2,3... etc enabling you to lay it out nicely in code).

![[Pasted image 20241025000057.png]]
![[Pasted image 20241025000104.png]]
what an unbelievably relatable interaction.

$M3 \cdot M2 \cdot M1 \cdot v$  ---> this is a *column-major* transformation mathematically.
$v \cdot M1 \cdot M2 \cdot M3$  ---> this is a *row-major* transformation.