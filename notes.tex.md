# Monkey cube

## Problems to consider
1. How long, on average, does it take to solve the cube from a random starting position?
2. How long does it take for it to be 'sufficiently mixed'?
[ in the future - add the technical names for this ]

## Thoughts so far...
1. Start simply: instead of the 3x3 cube, try a 1x1 cube.
2. Wow, that's hard. Start simpler: a triangle.
3. Write out the expected values for each state
4. Solve with a clever equation substitution. $\mathbb{E}(R_3)=\frac{4}{3}$
5. Extend to a square. Write the transformations as a matrix.
6. Solve matrix by hand first. Consider larger shapes. Write code.
7. Predict it will be Pascal's triangle, with one subtracted. Write it out as a triangle.
8. Be wrong. Discover it's a times table.
9. Justify why it's a times table parabola and nothing else other than a parabola.
10. Write a closed form solution for the average time for a polygon [ring?] as $\mathbb{E}(R_n)=\frac{n^2-1}{6}$
11. Consider a tetrahedron or a cube. Draw dots on a paper cube.

## Todos...
- Plot some graph of a cube and the ways it can be solved.
- Convert the transition graph of a cube into a matrix and solve it.
- Consider a 2x2x1 cube where corners can be swapped. Build from there?




