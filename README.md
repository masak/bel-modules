# bel-modules

A module mechanism for pg's Bel; allows you to do modular programming in Bel

## Later musing

I was thinking about this one.
The proposed solution neatly solves a particular part of the problem (herding global definitions that happened in a file into a "module object").

But arguably the whole challenge of modules is bigger than that.
I would phrase it like this:

> At the beginning of a module, you're guaranteed a **pristine** Bel environment.

The operative word, **pristine**, is defined so that all of the Bel "extension points" are guaranteed to be in their original state:

* Reader/`syntax`
* Bel evaluator/`bel`/`forms`
* Printer
* Types of literals/`lit`
* Comparisons/`comfns`
* Virtual functions/`virfns`
* Primitives/`prims`
* Named characters/`namecs`
* Templates/`templates`
* Buffers/`cbuf`/`bbuf`

(I might have missed some.)

Summarizing this, from the point of view of the module loader executing the module, it's as if a global _reset_ to the environment has taken place.
This reset needs to be rolled back after module execution has finished, such that the "caller" module also notices no adverse effects in its environment.

Of course, the export mechanism should then be capable enough so that if you _want_ to unyhgienically affect your caller, you can.
