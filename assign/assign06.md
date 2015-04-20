---
layout: default
title: "Assignment 6: Snake"
---

**Due**: Tuesday, May 5th by 11:59 PM

# Getting Started

Start by downloading [CS101\_Assign06.zip](CS101_Assign06.zip), saving it in the CS101 directory within your home directory.

Start a Cygwin Bash Shell (or Linux terminal, or MacOS terminal) and run the following commands:

    cd h:
    cd CS101
    unzip CS101_Assign06.zip
    cd CS101_Assign06

(Note that you should omit the cd h: step on Linux and MacOS.)

Using a text editor (e.g., Notepad++), open the file 

    CS101/CS101_Assign06/Snake.cpp

You will add your code to this file.

# Your Task

Your task is to implement a [Snake](http://en.wikipedia.org/wiki/Snake_%28video_game%29) game:

> ![snake game](images/snake.gif)

The play controls a snake.  The snake consists of some number of segments.  At each time step, the snake's head segment moves up, right, down, or left, and the other segments of the snake follow.  The player can control the direction of the snake's head using the arrow keys.  At all times, there is a piece of fruit on the playing field.  If the snake eats the fruit (i.e., the snake's head segment reaches the fruit), the snake grows by one segment.  When the fruit is eaten, a new piece of fruit appears in a random location.  If the snake's head goes out of bounds, or if the snake's head collides with one of the snake's body segments, the game is over.

You will use the terminal graphics functions: see [Lab 17](../labs/lab17.html), [Lab 18](../labs/lab18.html), [Lab 20](../labs/lab20.html), and especially [Lab 22](../labs/lab22.html).

# Hints, specifications, and requirements

## Playing field

The playing field should be 80 characters wide by 23 characters high.  The 24<sup>th</sup> row of the terminal should be used to display the player's current score and how many segments the snake has.

## `struct Scene`, `main` function

The starting code has a `struct Scene` data type and an example `main` function.  You should add fields to `struct Scene` to represent the current game state.  **Important**: you may *not* modify the `main` function.  This means that you must define `scene_init`, `scene_render`, and `scene\_update` functions that can work with the code in the `main` function.

## Defining struct types and functions

You should define struct data types and accessor functions as necessary to implement the game functionality.  For example, in my solution, I defined **struct Point** and **struct Snake** data types.  I also defined the following functions:

{% highlight cpp %}
void point_init(struct Point *p, int x, int y);
void snake_init(struct Snake *snake);
void snake_append_segment(struct Snake *snake, int x, int y);
void snake_remove_tail(struct Snake *snake);
struct Point snake_get_head(const struct Snake *snake);
struct Point snake_get_segment(const struct Snake *snake, int index);
{% endhighlight %}

## Implementing the snake

A good way to represent the snake is using an array of segments, such that each segment contains an x/y coordinate pair.  Because the number of segments varies (increasing each time the snake eats a piece of fruit), the snake struct type should use a counter field to keep track of how many segments there are.  The snake struct type should also keep track of which direction the snake is moving in.  Here is how I defined my `struct Snake` data type.

<!-- vim:set wrap: ­-->
<!-- vim:set linebreak: -->
<!-- vim:set nolist: -->
