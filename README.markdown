Concurrent Maze Space Transformation (with Authentic Interrodent Communication) in the HUNTER Programming Language
------------------------------------------------------------------------------------------------------------------

It is perceived that one of the biggest problems in maintaining interest
in programming is the above linear growth of boredom compared to the
usefulness of the program, resulting in an acute loss of enthusiasm on
the part of the programmers and ultimately the abandonment of the
software.

This document intends to address that by introducing a language with new
models for sharing, flow control, and data manipulation, which make all
dependencies in a program globally accessible and radically oblique at
the language level.

We introduce the language, which is a deterministic particle automaton
based on mazespace-rewriting and critter-style message passing and,
being ASCII art, is inherently graphical in notation...

The HUNTER Programming Language
===============================

©2000-2007 Cat's Eye Technologies. All rights reserved.

Each HUNTER program consists of a two-dimensional Cartesian-grid
playfield of any reasonable arbitrary size. Each square in this grid is
called a cell. Each cell may contain one of several things, or be
considered 'empty'. It may also contain a mouse, which is a particularly
special kind of thing. However, a mouse must start in an otherwise empty
square.

Mice are particularly special because they have agency. Unlike walls and
pieces of cheese, they do things. Primarily, they move around. They do
so at runtime.

The deterministic fashion a mouse moves around — always checking east,
then north, then west, then south, in each cell — and its memory (each
mouse keeps a 'map' of where it's been in it's head and tries not to
backtrack unless there is nowhere else new to go) ensures that, given
some time, and all other things being equal, a mouse will traverse it's
entire environment and will return to where it started. The process then
repeats, holding the mouse in a state of perpetual live lock.

However, not all other things may be equal. Indeed, the mouse may nibble
on a bit of strychnine and die. Or, other mice may be concurrently
traversing the same maze, and two mice may not share the same space, so
they may block each other's progress.

Mice may not move through walls but they may move through empty space
and on top of items found in the playfield, possibly altering them (see
below.)

Execution ends when all mice are dead.

An example HUNTER program might be:

    ########
    #   1#2#
    # #### #
    #      #
    # ######
    #     m#
    #+######
    #     !#
    ########

where

-   `#` indicates a wall
-   `m` indicates a mouse
-   the digits `0` to `9` represent types of cheese:
    -   `0` = cheddar
    -   `1` = american
    -   `2` = swiss
    -   `3` = gouda
    -   `4` = mozzarella
    -   `5` = farmer
    -   `6` = blue
    -   `7` = gorgonzola
    -   `8` = feta
    -   `9` = bat's-milk

-   `!` indicates a bit of strychnine
-   `+` indicates a pinwheel
-   `.` indicates a mouse turd
-   `w` indicates a dead mouse carcass

All other characters indicate other miscellaneous objects apropos to
being in a maze, with undefined semantics, so they should be considered
reserved.

Intermouse communication is done by mouse droppings. A mouse can leave a
message to some other mouse by creating a mouse dropping where it
currently is (assuming it has previously eaten a piece of cheese.) Other
mice can detect mouse droppings and change their behaviour based on
them.

How mice create droppings is defined by how each mouse is trained. These
mice are somewhat magical in that they can be trained to perform
physically improbable tasks, such as turning one kind of cheese into
another.

Mice are trained globally by the mazespace-rewriting rules. These are
the guidelines by which rodents live their lives. Each rule must be on a
line by itself and has the following form:

    *things>droppings

For example,

    *12>21

Then, when a mouse encounters a piece of American cheese, followed by a
piece of Swiss cheese, it will eat them and excrete a bit of Swiss
cheese followed by a bit of American cheese. This is just an example.

Mice will eat cheese but will not eat mouse droppings, pinwheels, or
other inedible items.

Specifying strychnine, walls, or mice on the left-hand side of a
rewriting rule is not guaranteed to be able to produce a match. The
behaviour of specifing mice on the right-hand side of a rewriting rule
is undefined.

Implementation
--------------

There is an implementation of HUNTER in Perl 5. It requires the
[Console::Virtual](http://catseye.tc/projects/console-virtual/) module
to run; however, this module is included in the HUNTER distribution, so
you shouldn't have to worry about that.

Chris Pressey  
Winnipeg, Manitoba, Canada  
Original Oct 24 2000  
Revised for clarity Jan 26 2002  
HTML'ized Nov 23 2007  
Markdownified Jun 22 2012
