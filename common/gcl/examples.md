# GCL examples

Various excerpts of GCL are collected here for the purpose of serving as syntax examples.

## Metal Gear Solid

Fragments of the game's GCL source files (along with other code and data) were embedded into the game's overlays for an unknown reason. Unfortunately, in many cases these fragments are not only incompletely but partially corrupted.

| Fragment | Version | Offset in STAGE.DIR | Edited? |
| ----- | ----- | ----- | ----- |
| [mgs1_fragment01.gcl](examples/mgs1_fragment01.gcl) | MGS Integral (VR Disc) | 0x01d7b650 | Yes |
| [mgs1_fragment02.gcl](examples/mgs1_fragment02.gcl) | Japan (Disc 1/2) | 0x00865b58 | Yes |
| [mgs1_fragment03.gcl](examples/mgs1_fragment03.gcl) | North America v1.1 (Disc 1/2) | 0x03ee84cc | No |
| [mgs1_fragment04.gcl](examples/mgs1_fragment04.gcl) | MGS Special Missions | 0x02b99738 | No |
| [mgs1_fragment05.gcl](examples/mgs1_fragment05.gcl) | MGS Special Missions | 0x02d95cd0 | Yes |
| [mgs1_fragment06.gcl](examples/mgs1_fragment06.gcl) | MGS Special Missions | 0x0399b660 | No |

Files have been edited in an attempt to restore lost information.

Note: For display purposes, text encoding has been changed from EUC-JP to UTF-8. Null bytes in places that could not be restored have been replaced with ``[NUL]``.

## Metal Gear Solid 2

The Document of MGS2 provides a description of how the language operates and an example of the actual code.

>The GCL (Game Command Language) is the script language designed for the development of MGS. It is a very versatile language. The contents of the script can be divided up into those for "program startup" and "event setting."
In MGS, programs other than the system are designed as "parts" that can be started up by the Script Unit when putting together a stage. For example, the "player", "enemy soldier", "surveillance camera", and "door" are all "parts" that can be assigned positions and parameters freely when starting up the stage.
Individual effects are also treated as parts whose parameters can be adjusted freely.
"Event setting" pertains to orders causing events to happen when the player or enemy steps into or out of a predetermined area. For example, "the door will open when the player steps in front of the door" is such an order. In other words, a message is sent so that the "parts" programs that have already been started up perform their functions. These messages are predetermined.
Here is an actual example.
```
chara ドア DoorA1 \
	-kms std_door \
	-position 9325,0,-5050 \
	-rotate 0,2048,0

trap DoorA1_Area スネーク \
	-mask 入る \
	-exec {
		mesg ドア DoorA1 open
	}
```
>The portion beginning with "chara" is what calls for a "parts" program. Such portions are give specific names ("DoorA1" in this case). The parameters assigned are the name of the door model, position, and rotation angle. All of this makes a door show up in a certain position in the game.
The portion beginning with "trap" is what "sets an event". When "スネーク" (Snake) enters the area designated as "DoorA1_Area" by another tool, the execution block beginning with "exec" sends an "入る" (open) order to the "ドア" (door) program called "DoorA1".
Other situations involve multiple "condition forks" that change what happens depending on the circumstance. The entire game is pretty much composed of combinations of these parts and event sets. It might be fun to play the game trying to guess what kind of script governs each item position, camera behavior, and individual event you experience.

## Metal Gear Solid 4

#### From "[Hideo Kojima's Gene](https://youtu.be/FWykspO8Gyc?t=67)"

Footage of GCL from the game was briefly shown on-screen.

See: [mgs4_making.gcl](examples/mgs4_making.gcl)

Note: This example may contain errors as it was copied by hand from a somewhat blurry screen. ([Image 1](examples/mgs4_making_a.jpg)) ([Image 2](examples/mgs4_making_b.jpg))

#### From CEDEC 2008 presentations

Collected from PowerPoint slides presented at CEDEC 2008.

See: [mgs4_cedec2008_1.gcl](examples/mgs4_cedec2008_1.gcl)

See: [mgs4_cedec2008_1.gcl](examples/mgs4_cedec2008_1.gcl)