# Adventure: introduction

In this project, your goal is to implement **Crowther's Adventure game** using OOP in Python. Eventually, your project will be implemented in a number of separate files that each contain some part of the code. Practicing with the design of programs using OOP is the main goal of this project. For most parts, we offer strong guidelines on how to implement your code; but for other parts, figuring out how to fit new functionality is your responsibility.

> All parts of this final assignment are to be done individually. Feel free to discuss programming strategies and overall design with other students, but refrain from diving into specifics about how to write code for particular parts of the program.

## Background

Back in the days, before computer graphics on personal computers (PCs) were a thing, text-based adventure games were incredibly popular. This type of game consists entirely out of text printed to the screen, and is traversed by typing in commands, much like those one would enter in the terminal to navigate the file system.

One such game is Colossal Cave Adventure, created by [William Crowther](https://en.wikipedia.org/wiki/William_Crowther_(programmer)) in 1975. This game served as an inspiration for all of the text adventure game genre. The commands that a player enters in Adventure can be words like "IN" and "OUT", or maybe "WEST" and "EAST", each suggesting a direction that is taken to navigate the "virtual world".

Here is an example where the player is displayed a description of the current place in the virtual world, then they enter a command which leads to another place (or "room"), and so on:

    You are standing at the end of a road before a small brick
    building. A small stream flows out of the building and
    down a gully to the south. A road runs up a small hill
    to the west.
    > WEST
    You are at the end of a road at the top of a small hill.
    You can see a small building in the valley to the east.
    > EAST
    Outside building.
    >

So, the essence of such a game is a loop that prints descriptions and allows user input. Together, all the places in the virtual world can be mapped out to get an idea of how everything is connected. The very first part of the adventure "map" may look like this:

![](../../map.png){:.w300}

You can find a full map, including a spoiler-free version, [at this website](http://www.spitenet.com/cave/).

The adventure "map" is provided in a few **data files** that contain room names and description, and in particular, information about which rooms are connected to other rooms, and using which commands. None of this information is "hard coded" into the program!

And there is more than just navigating: at all times a player can ask for `HELP` to get an explanation of the game, or `LOOK` to get a detailed description of the room they are in.
If you've carefully studied the previous example, you could have seen that the second time a room is entered, a shorter description is shown. If we were to enter the `LOOK` command we would again see the following:

    > LOOK
    You are standing at the end of a road before a small brick
    building. A small stream flows out of the building and
    down a gully to the south. A road runs up a small hill
    to the west.
    >

Though William Crowther originally wrote his game in Fortran, an imperative programming language that has been around since the 1950s, we will be taking a more modern approach to its implementation, using object-oriented programming (OOP). OOP is particularly suited to Adventure, because we can model the whole game as a series of interconnected "room" objects.


## Specification

Implement an object-oriented version of Crowther's Adventure game using the class structure provided in the assignment. The main features of the game are the following:

1. **loading** of the map:
    * handling command line arguments to open a given datafile
    * loading map data into a series of objects
2. **user interaction**:
    * prompting the user for commands and execute those
    * warn about non-existent commands
    * moving the player from room to room
3. **game logic**:
    * forced movements
    * managing items and inventory


## Understanding

Download the starter code along with a few versions of the game data:

    $ cd ~/problems
    $ wget https://github.com/minprog/adventure/raw/2022/steps/adventure.zip
    $ unzip adventure.zip
    $ rm adventure.zip
    $ cd adventure
    $ ls
    adventure.py  data/

### Game data

The `data` directory contains data files with which you can create two versions of adventure. `TinyAdv.dat` is the smallest adventure game, consisting of 4 rooms. Here are its contents in full:

    1	Outside building	You are standing at the end of a road before a small brick building.  A small stream flows out of the building and down a gully to the south.  A road runs up a small hill to the west.
    2	End of road	You are at the end of a road at the top of a small hill. You can see a small building in the valley to the east.
    3	Inside building	You are inside a building, a well house for a large spring.
    4	Victory	You have found the hidden well of winning a tiny game. Congratulations!

    1	WEST	2	UP	2	NORTH	3	IN	3
    2	EAST	1	DOWN	1
    3	SOUTH	1	OUT	1	DOWN	4

    KEYS	a set of keys	3
    LAMP	a brightly shining brass lamp	2

The file has three parts, divided by two blank lines. The first part describes the "rooms", with on each line an identifying number, then a TAB character, then a short description, then another TAB character, and then a long description:

    1	Outside building	You are standing at the end of ...

The second part describes connections between rooms. In fact, this section defines the "commands" that players can type to navigate from one room to another. Of each line, the first part is a room identifier (the place where the connection starts) and then there are one or more connections, each having a command, then a TAB, and the number of the room it connects to.

    2	EAST	1	DOWN	1

The third and final part describes "objects" that may be found in the game. Each line contains a "command" that can be typed to manipulate the object, then a TAB, then a short description of the object, then a TAB and finally the number of the room that the object will initially be placed in.

Also included in your distribution is `SmallAdv.dat`, which is a bit larger and includes more advanced interactions, as well as `CrowtherAdv.dat`, which is the complete original adventure game!


### Starter code

Take a look at `adventure.py`. The file has two parts.

1. The `Adventure` class contains all methods that make the game work:

	- The `__init__` method ensures that all is set for playing an adventure game. In particular, it calls a method (that does not exist yet) to load game data.

	- The `room_description` method provides the description of the current room, the room the player is in. (It also calls a method that does not exist yet.)

	- Moving around in the game is handled by the `move` method, by setting the "current" room to a different one.

2. The `if __name__ == "__main__"` part, which contains the main "game loop" of the program. After introducing the game, it repeatedly asks for a command from the user, and tries to perform that command. The actual handling of the commands is coded into the `Adventure` class, so the main responsibility of this part is to perform the game loop and translate commands into method calls to an `Adventure` object.

Make sure that you understand every line of code in `adventure.py` before you start. Think about the methods that do not exist yet: what is their responsibility in making the game work?

> A hard constraint in this program is that the `Adventure` class may not `print` anything. All printing should be done in the `__main__` part. And in return, the `__main__` part may, aside from printing things, only call methods in the `Adventure` class. It may not access methods and/or attributes from other classes that you will be writing. As such, each class will have separate responsibilities.
