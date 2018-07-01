# Introduction

Monkeys solving cubes.

## Getting a sesne for the problem

Discuss these 'moves' and 'states' and their symmetries. Discuss the rules: randomly pick a starting state, randomly pick from the moves available to you

# Start Simpler
A 3x3x3 Rubik's cube is pretty complex. Can we start simpler?

[image of 2x2x2 cube]

No, even simpler.

[image of 1x1x1 cube]

Think even simpler.

[image of square]

Just a little farther...

[image of triangle]

There we go! We'll start by thinking about a triangle. A triangle can be in one of three conditions:


      •          ^         ^
     /1\   or   /2\   or  /3\
    -----      •----     ----•

The Rubik's cube has a lot of moves. We'll give ourselves exactly two moves: rotate clockwise by 120 degrees, or rotate counterclockwise by 120 degrees. [Todo: why?]

[maybe add a table about what the rotations do?]

# Considering the Triangle

Recall the question we're answering. On average, how many random moves will it take to solve a randomly mixed up Rubik's cube? How does that translate into a triangle? We'll call the 'solved' state the triangle where the dot is on top. Number 1, to be precise. Our moves are one of two: either rotating clockwise, or rotating counterclockwise.

We're going to solve this question in two steps. First, we calculate, for each of the three states, how long it takes on average to be solved. Then, we consider the average of all of them, because the state we start out in is randomly chosen from all possible states.

## How many steps from Triangle 1? 2? 3?

The first triangle is easy. It's in state 1, which is already the solved state. We use exactly 0 moves to solve that triangle. In symbols, I say that $$M_1 = 0$$. You can read $$M_1$$ as "the number of **M**oves to solve triangle **1**", and so $$M_1 = 0$$ means "The number of moves to solve triangle 1 is 0."

Now let's consider what will happen from triangle two. It's clear that we'll need at least one random move. Then, with the random move, there are two options. Either it becomes like triangle 1, or like triangle 3, both with probability 1/2. After that, the the number of random moves to solve the triangle are the very numbers we're calculating. No worries - we'll figure those numbers out in a bit. For now, let's write our equation using the $$M$$ variables.

$$M_2 = 1 + \frac{1}{2}M_1 + \frac{1}{2}M_3$$

We follow a similar idea for calculating $$M_3$$. Either triangle 3 rotates clockwise to triangle 2 or counterclockwise to triangle 1. We need at least one random move, plus however many random moves it takes to solve the triangle from wherever we end up.

$$M_3 = 1 + \frac{1}{2}M_1 + \frac{1}{2}M_2$$

Now we can substitute our equation for $$M_3$$ into the equation for $$M_2$$.
 [sidebar - how did i think to substitute?]

$$M_2 = 1 + \frac{1}{2}M_1 + \frac{1}{2}(1 + \frac{1}{2}M_1 + \frac{1}{2}M_2)$$

Remember, $$M_1 = 0$$, so we can take those terms out.

$$M_2 = 1 + \frac{1}{2}(1 + \frac{1}{2}M_2)$$

Multiply out,

$$M_2 = 1 + \frac{1}{2} + \frac{1}{4}M_2$$

combine like terms,

$$\frac{3}{4}M_2 = \frac{3}{2}$$

and divide.

$$M_2 = 2$$

With that value, we can solve for what $$M_3$$ is too.

$$M_3 = 1 + \frac{1}{2}M_1 + \frac{1}{2}M_2$$

$$M_3 = 1 + 0 + \frac{1}{2}(2)$$

$$M_3 = 2$$

[sidebar: Why are $$M_2$$ and $$M_3$$ both 2? think symmetry]

## How many steps from a randomly selected triangle?

We have three triangles: 1, 2, and 3. Each of them, as we discussed above, have the same probability of being selected, which must be $$\inline{\frac{1}{3}}$$. Once we randomly choose a triangle, we know how long, on average, it takes to be solved. With $$M_{\triangle}$$ representing the number of moves from a randomly chosen triangle, we can write:

$$M_{\triangle} = \frac{1}{3}M_1 + \frac{1}{3}M_2 + \frac{1}{3}M_3$$

$$M_{\triangle} = 0 + \frac{2}{3} + \frac{2}{3}$$

$$M_{\triangle} = \frac{4}{3}$$

# Moving Up to a Square

Next, we consider a square. 

[what can you do with a square? aka how much do you rotate it.]

We can try solving it the same way we did the triangle - with systems of equations. However, we'll have a lot of equations. 

One thing to notice, though, is that we've got a *linear system of equations*, which is really well suited for *linear algebra*. 

[Sidebar: what is linear algebra?]
[Sidebar: how does one realize this?]

## As a Matrix

All of the equations have the form 

$$M_n = 1 + \frac{1}{2}M_{n-1} + \frac{1}{2}M_{n+1}$$

We can rearrange this to 

$$-\frac{1}{2}M_{n-1} + M_n + -\frac{1}{2}M_{n+1} = 1$$

also, if we pay attention, let's take out the references to M_1 because it's zero.

With a square, we get the equations: [notice the spacing]

$$\begin{matrix}
M_2 & -\frac{1}{2}M_3 & & = 1 \\
-\frac{1}{2}M_2 & + M_3 & -\frac{1}{2}M_4 & = 1 \\
& -\frac{1}{2}M_3 & + M_4 & = 1 \\
\end{matrix}$$

This is equivalent to the matrix equation:

$$\begin{bmatrix}
               1 & -\frac{1}{2} &            0 \\
    -\frac{1}{2} &            1 & -\frac{1}{2} \\
               0 & -\frac{1}{2} &            1
\end{bmatrix}
\begin{bmatrix} M_2 \\ M_3 \\ M_4 \\ \end{bmatrix}
=\begin{bmatrix} 1 \\ 1 \\ 1 \\ \end{bmatrix}
$$

This can be solved pretty quickly by a computer program.

What's nice about this is that it's a simple pattern. If we have a pentagon, for example, and we're rotating by 72 degrees, we have the matrix:

$$\begin{bmatrix}
               1 & -\frac{1}{2} &            0 &            0 \\
    -\frac{1}{2} &            1 & -\frac{1}{2} &            0 \\
               0 & -\frac{1}{2} &            1 & -\frac{1}{2} \\
               0 &            0 & -\frac{1}{2} &            1 \\
\end{bmatrix}
\begin{bmatrix} M_2 \\ M_3 \\ M_4 \\ M_5 \end{bmatrix}
=\begin{bmatrix} 1 \\ 1 \\ 1 \\ 1 \end{bmatrix}
$$

and more generally, we have, for a n-sided polygon, with two rotations only, we have:

$$\begin{bmatrix}
               1 & -\frac{1}{2} &            0 &        \dots &            0 \\
    -\frac{1}{2} &            1 & -\frac{1}{2} &        \dots &            0 \\
               0 & -\frac{1}{2} &            1 &        \dots &            0 \\
          \vdots &       \vdots &       \vdots &       \ddots & -\frac{1}{2} \\
               0 &            0 &            0 & -\frac{1}{2} &            1 \\
\end{bmatrix}
\begin{bmatrix} M_2 \\ M_3 \\ M_4 \\ \vdots \\ M_n \end{bmatrix}
=\begin{bmatrix} 1 \\ 1 \\ 1 \\ \vdots \\ 1 \end{bmatrix}
$$

## Considering Python Code

[write the code, explain later]

```
import numpy as np
def build_moves_matrix(n):
    # n is the size of the matrix
    matrix = np.diag(np.ones(n))
    negative_halves = np.repeat(-.5, n-1)
    matrix += np.diag(negative_halves, 1) + np.diag(negative_halves, -1)
    return matrix

print build_moves_matrix(5)
```
sanity check that it's working.

```
ring_size = 4
moves = build_moves_matrix(ring_size - 1)

weights = np.linalg.solve(moves, np.repeat(1, ring_size - 1))

print 'weights: {}'.format(weights)
print 'average walk: {}'.format(sum(weights) / ring_size)

n = ring_size
print (n*n - 1)/6.
```















