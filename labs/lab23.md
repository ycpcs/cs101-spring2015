---
layout: default
title: "Lab 23: Mini Golf"
---

# Getting Started

As always, you may refer to [Lab 1](lab01.html) if you need a reminder about how to start the **Cygwin Bash Shell** or **Notepad++**.

Begin by downloading [CS101\_Lab23.zip](CS101_Lab23.zip). Save the zip file in the **H:\\CS101** directory.

Start the **Cygwin Bash Shell** and run the following commands:

    cd h:
    cd CS101
    unzip CS101_Lab23.zip
    cd CS101_Lab23

Start the **Notepad++** text editor. Use it to open the files

> **H:\\CS101\\CS101\_Lab23\\MiniGolf.cpp**

When you are ready to compile the program, in the Cygwin window type the command

    make

To run the program, in the Cygwin window type the command

    ./MiniGolf.exe

# Your task

Your task is to complete the program so that it simulates a game of mini golf.

Here is an animation showing what the completed game will look like:

> ![mini golf](images/lab23/minigolf.gif)

First, the player positions the ball using the up and down arrows.  Then, the player presses "j" or "k" to hit the ball.  ("j" hits up and to the right, and "k" hits down and to the right.)  The ball bounces around in much the same manner as labs [18](lab18.html), [20](lab20.html), and [22](lab22.html).  One additional detail is that there is a center obstacle that the ball can bounce off of.  If the ball reaches the cup, the player wins and the program displays "Hole in 1!!!".

# Implementation

## Data representation

The overall game state is represented by the `struct Scene` data type.  This data type uses `struct Point`, `struct Ball`, and `struct Rect` data types, as follows:

{% highlight cpp %}
struct Point {
	int x, y;
};

struct Ball {
	struct Point pos;
	int dx, dy;
};

struct Rect {
	struct Point topleft;
	int width, height;
};

struct Scene {
	struct Rect obstacle;
	struct Rect cup;
	struct Ball ball;
	int mode; // game mode
};
{% endhighlight %}

You will not need to modify these struct types.

## Functions

The following functions operate on these data types:

## Step 1: Implement functions
