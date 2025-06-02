This is my configuration for tintin++ to play the MUD hosted at tdome.nukefire.org (formerly at tdome.net).  I have tried to break things down into modular components.  I hope it is not difficult to customize, but the code is for my character, my play style, and my OS environment.

# installation

This repo should be cloned to:

    ~/.tintin/config

This is MY config, and it will probably not work for you without modification.  Set your username, to start.  Find that here:

    config/tdome/settings.tt

The current working directory is expected to be `~/.tintin`.  This is how I launch the game:

    alias tdome='(cd ~/.tintin/; tt++ config/tdome.tt)'

# fighting

Many automatic responses are defined here:

    config/tdome/operations/fight.tt

These should form a loop, once an enemy is targeted.  The gist is to avoid or disengage from direct combat and to engage in sneak attacks.  That would probably be simpler for a tank class.  It would probably be differently complex for a healer class.  Either is left as an exercise to the reader.

# patrol mode

Set some patrol points here:

    config/tdome/automation/patrol/definitions.tt

Set the patrol timing variables here:

    config/tdome/settings.tt

Enter `p` (lower case) to enter patrol mode.  Your character should pace among the patrol points without help, if:

  * The points are mapped.
  * The way is not blocked.  (Doors.)
  * You are not attacked.
  * Nothing else wrong or unexpected happens.

See `predation mode` for compatibility notes.

# predation mode

Define your prey of choice here:

    config/tdome/automation/prey/code.tt

Enter `P` (upper case) to enter Predatation mode.  Your character will attempt to jump any mob defined as prey.  You will automatically stay locked on to one target until it is dead, at which point you will seek a new target.

This should be compatible with patrol mode.  Your character will remain stationary as long as you have a designated target.  Once the target is eliminated, patrol will resume.

# autoloot

There is some code to automatically loot from fallen enemies.  This may no longer be necessary, as nukefire seems to have an in-game autoloot system, and it seems to be on by default.

# mapping

Mapping should be on by default.  Mapping the spawn point for new characters can be tricky, but if you use the existing world map this should should already be done.  There is not yet handling for more than one map file, but this may be necessary if you cross an ocean or something.

Mapping should work while following another player.

Mapping is not expected to work while riding a vehicle.  I need to check on whether riding a vehicle gives some kind of consistent message about movement and direction, in which case this can be added.

Enter `M` (upper case) to toggle mapping.  Turning it off will avoid creating bad maps if you are in a situation that doesn't map well.  If you are in a maze that gets randomly generated every time you enter, for example, you should probably avoid mapping that.  It also helps to turn of mapping at times while trying to connect asymmetric parts of a large map.

If you have explored, and you are satisfied with the additions to the map, enter 'mw' (lower case) to save your changes.  By default, they will DISAPPEAR WITH NO WARNING when you terminate tintin.

Mapping is complex.  Read the documenation for tintin to see how to link rooms, create void space between rooms, and otherwise handle asymmetries and peculiarities of the in-game map in your out-of-game map file.

# self-care

There is some old code handling automatic eating and drinking.  It was due for a rewrite, but may be unnecessary, now.  Nukefire seems to not require characters to eat, drink, or sleep.  That seems unfortunate to me; I wanted to get this part right.

# buy

There is an alias to override the `buy` command to buy multiple things.  That breaks buying tattoos and implants, at least.  `#unalias buy` to turn that off.  Nukefire's implementation of the `buy` command should be observed to determine whether this alias is still beneficial.
