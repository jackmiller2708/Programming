> Objects bind functions and data structures together in indivisible units. I think this is a fundamental error since functions and data structures belong in totally different worlds. — [Joe Armstrong](http://harmful.cat-v.org/software/OO_programming/why_oo_sucks), creator of Erlang

Objects (or nouns) are at the very core of OOP. A fundamental limitation of OOP is that it forces everything into nouns. And not everything should be modeled as nouns. Operations (functions) should not be modeled as objects. Why are we forced to create a `Multiplier` class when all we need is a function that multiplies two numbers? Simply have a `Multiply` function, let data be data and let functions be functions!

In non-OOP languages, doing trivial things like saving data to a file is straightforward — very similar to how you would describe an action in plain English.

> Real-world example, please!

Sure, the painter owns a `PaintingFactory`. He has hired a dedicated `BrushManager` , `ColorManager`, a `CanvasManager`  and a `MonaLisaProvider`. His good friend zombie makes use of a `BrainConsumingStrategy` . Those objects, in turn, define the following methods:  `CreatePainting` , `FindBrush` , `PickColor` , `CallMonaLisa` , and `ConsumeBrainz`.

Of course, this is plain stupidity, and could never have happened in the real world. How much unnecessary complexity has been created for the simple act of drawing a painting?

There’s no need to invent strange concepts to hold your functions when they’re allowed to exist separately from the objects.