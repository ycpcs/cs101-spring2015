---
layout: default
title: "Assignment 5: Conway's Game of Life"
---

**Due**: TBD

# Getting Started

Start by downloading [CS101\_Assign05.zip](CS101_Assign05.zip), saving it in the CS101 directory within your home directory.

Start a Cygwin Bash Shell (or Linux terminal, or MacOS terminal) and run the following commands:

    cd h:
    cd CS101
    unzip CS101_Assign05.zip
    cd CS101_Assign05

(Note that you should omit the cd h: step on Linux and MacOS.)

Using a text editor (e.g., Notepad++), open the file 

    CS101/CS101_Assign05/GameOfLife.cpp

You will add your code to this file.

# Your Task

In this assignment, you will implement a simulation of [Conway's Game of Life](http://en.wikipedia.org/wiki/Conway%27s_game_of_life), also known as simply *Life*.  Life is a simulation of simple one-celled organisms on a two-dimensional grid.

The simulation starts with an initial generation of cells, and then proceeds by repeatedly computing the next generation based on the current generation.

As each new generation is computed, cells either live or die according to the Rules of Life:

* if a cell is alive in the current generation, but has fewer than 2 neighbors, it dies of isolation
* if a cell is alive in the current generation, but has more than 3 neighbors, it dies of overcrowding
* if a cell is dead in the current generation, and has exactly 3 neighbors, it is born

The neighbors of a cell are the 8 cells immediately surrounding it.

## Data Representation

The current generation of cells is stored in the `board` array, defined in the `main` function:

{% highlight cpp %}
int board[HEIGHT][WIDTH];
{% endhighlight %}

The `HEIGHT` and `WIDTH` constants are defined near the top of the file, and define the number of rows and columns of cells (20 and 60, respectively).

Each array element represents one cell.  Alive cells are represented as 1 values, and dead cells are represented as 0 values.

## Functions

Your program should implement and use the following functions:

{% highlight cpp %}
void init_random_board(int board[HEIGHT][WIDTH]);
void print_board(int board[HEIGHT][WIDTH]);
int get_cell(int board[HEIGHT][WIDTH], int row, int col);
int count_neighbors(int board[HEIGHT][WIDTH], int row, int col);
void compute_next_gen(int board[HEIGHT][WIDTH]);
{% endhighlight %}

Prototypes are provided.

The `init_random_board` function should assign a random 0 or 1 value to each element of the array passed as a parameter, such that the probability of setting a cell to 0 is .75, and the probability of setting a cell to 1 is .25.  (In other words, about 75% of the cells should be 0, and about 25% of the cells should be 1.)

The `print_board` function should print a textual representation of the cells contained in the array passed as a parameter.  Each alive cell should be represented by an asterisk (\*), and each dead cell should be represented by a period (.).

The `get_cell` function should return the value of the cell whose row and column are specified.  As a special case, if either the specified row or column is out of bounds, the function should return 0.

The `count_neighbors` function should return a count of the total number of alive neighbors of the cell whose row and column are given.  There is one important special case: cells at the edges of the array will have fewer than 8 neighbors.  Nonexistent neighbors should be considered to have a value of 0.  **Hint**: Call the `get_cell` function, since it automatically returns 0 when called with the row and column of a nonexistent cell.

The `compute_next_gen` function should update the array passed as the parameter so that it contains the next generation of cell values according to the rules.  **Hint**: Use a second array to store the computed values for the next generation, and then copy them into the parameter array.  This approach is similar to the one recommended in [Lab 16](../labs/lab16.html).

## Running the program

When the program starts, it will prompt the user to either load initial game data from a file, or generate a random initial game state (by calling your `init_random_board` function.)  It will also prompt the user for a number of generations to simulate.

You should modify the program so that it:

1. Prints the initial game state (using the `print_board` function)
2. Simulates the specified number of generations
3. Prints the final game state (again, using the `print_board` function)

Here is an example run:

<pre>
(0) Load from file, or (1) initialize random board? <b>0</b>
Name of file to load: <b>glider.dat</b>
How many generations? <b>33</b>
Initial board:
............................................................
...*........................................................
.*.*........................................................
..**........................................................
............................................................
............................................................
............................................................
............................................................
............................................................
............................................................
............................................................
............................................................
............................................................
............................................................
............................................................
............................................................
............................................................
............................................................
............................................................
............................................................
Final board:
............................................................
............................................................
............................................................
............................................................
............................................................
............................................................
............................................................
............................................................
............................................................
..........*.................................................
...........**...............................................
..........**................................................
............................................................
............................................................
............................................................
............................................................
............................................................
............................................................
............................................................
............................................................
</pre>

<!-- vim:set wrap: ­-->
<!-- vim:set linebreak: -->
<!-- vim:set nolist: -->

