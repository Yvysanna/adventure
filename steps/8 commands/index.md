# Adventure: additional commands

`HELP` and `LOOK` are two commands to make the game a bit easier to use.


## What to do

Implement the additional commands in the following way:

-   `HELP` prints instructions to remind the player of their commands and how to use them. It should behave as follows:

		> HELP
		You can move by typing directions such as EAST/WEST/IN/OUT
		QUIT quits the game.
		HELP prints instructions for the game.
		LOOK lists the complete description of the room and its contents.
		INVENTORY lists all items in your inventory.

-   `LOOK` prints a long description of the room the player is currently in, even if the room was visited earlier.

		Inside building
		> LOOK
		You are inside a building, a well house for a large spring.
		KEYS: a set of keys

-	`INVENTORY` prints all items in the player's  inventory. It should behave as follows depending on what is in the inventory:

		> INVENTORY
		KEYS: a set of keys
		LAMP: a brightly shining brass lamp

		> INVENTORY
		Your inventory is empty
