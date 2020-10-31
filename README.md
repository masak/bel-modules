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

I might have missed some.

The main point is that the module file should be able to assume that no external script or module file has messed with its environment, that it's pristine.

Of course, the export mechanism should then be capable enough so that if you want to export changes to any of the above, you can.
