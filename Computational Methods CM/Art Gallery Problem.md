The art gallery problem is a geometric problem in which an uneven, concave polygon (i.e. 2D shape, though the problem also exists for 3D polyhedra but is much harder to solve) must have the minimum possible number of 'guards' posted at discrete points on or within the polygon such that the entire polygon is 'visible' to the guards (i.e. there is an unbroken ray that leads from any point on any edge to at least one guard). The problem specifically is finding the minimum number of guards.

The analogy is referential to an art gallery of course, with various rooms of different shapes, which is likely to be concave and possible have disconnected obstacles within the gallery. In this scenario, we need to be able to see the whole gallery at once to keep the artworks safe from theft or vandalism, while hopefully minimising the number of guards required to guard it at once. We assume that each guard has 360 degree vision.

Václav Chvátal showed that the maximum possible number of guards required was equal to $\frac{n}{3}$ , where $n$ is the number of vertices in the polygon. It can be seen that a single guard must be able to observe the whole of a convex shape (of which a triangle is the simplest and always convex), since no matter where within or on a triangle we place our observation point, we can draw direct lines to all the corners of the triangle. We can see therefore that Chvátal's theorem is true, because if we triangulate the polygon (i.e. we ensure the entire shape is made up of shapes of only 3 vertices) the maximum possible number of triangles we could end up with is $\frac{n}{3}$ , for the case where the gallery is made up of a number of disconnected triangles which share no vertices with one another, and since we need exactly one guard per triangle, we can then see that the maximum possible number of guards needed would be also $\frac{n}{3}$ [^1].

However, our number of guards is reduced when we consider that many triangles will share at least one vertex with a neighbour, usually sharing two with any particular neighbour, which reduces the number of guards required, saving one guard each time this happens. The difficulty of the art gallery problem lies in decomposing a complex shape with many 'ins and outs' and placing guards optimally.

Continuing this train of thought, it is true that we can triangulate our polygon and then colour each of its vertices one of three colours, such that all triangles have one of each of the three colours on it's vertices. Steve Fisk points out that by taking the total number of vertices of a certain colour, specifically the colour with the fewest instances in the polygon (i.e. in a polygon with 2 red, 1 green and 1 blue vertices, we would take either 1 green or 1 blue) we can reduce our maximum number of guards required[^2]. This is essentially a mathematical form of the 'sharing vertices' concept described in the previous paragraph.

Both of these geometric proofs are useful for reducing the search space in terms of finding solutions for smaller numbers of guards by setting an upper bound. However, these approaches are somewhat naive as they cannot optimise concave shapes where vertices are not shared. See the diagram below:
![[complicated_gallery.png]]
Chvatal's proof would tell us that we need a maximum of three guards (since we have seven total vertices, and we have to round up), and Fisk's proof and the colouring scheme tells us that we need at most two guards: these could be placed at the two green vertices, or the two blue ones. However, looking from above, we can clearly see that we only need to place a single guard at the highlighted green vertex. Everything that the other green vertex can see, can also be seen by the highlighted vertex, plus a bit more.

An algorithm to optimise this problem to minimise the number of guards would need to be able to look at different combinations of guard placements to see if the number of guards can be reduced (i.e. brute-force). Heuristics could be applied for example by counting around vertices and looking at their angles relative to the origin vertex to see if there are occluded (invisible from that point) areas. Approximation methods might use a grid to check the coverage of the polygon from certain vertices in the shape.

It's important to note that we have an additional constraint in this problem: keeping guards on vertices. However, there are variations of the problem (and indeed, real-world applications light lighting a stage would be less constrained) which allow guards to be placed on edges, or even anywhere within the polygon, massively (ordinally) increasing the search space, by way of the number of possible configurations.

One approach presented by Ghosh is to reduce the the overall polygon to a set of convex polygons, each of which may be observed by a single guard[^3]. However, even this may not produce optimal results, see the diagram above once again.

The problem, depending on constraints, is considered NP-hard, meaning it it's both difficult to solve and difficult to verify in polynomial (i.e. $O(n^t)$) time.

[^1]: Chvátal, V. (2004) _'A combinatorial theorem in plane geometry'_, _Journal of Combinatorial Theory, Series B_. Available at: https://www.sciencedirect.com/science/article/pii/0095895675900611 (Accessed: 29 October 2023).
[^2]: Aigner, M., Ziegler, G.M. (2018). _'How to guard a museum. In: Proofs from THE BOOK'_. Springer, Berlin, Heidelberg. https://doi.org/10.1007/978-3-662-57265-8_40
[^3]: Ghosh, S. K. (1987), _'Approximation algorithms for art gallery problems'_, _Proc. Canadian Information Processing Society Congress_, pp. 429–434.