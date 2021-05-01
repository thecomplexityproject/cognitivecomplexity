# The set of code snippets

> **Definition**
>
> A ***code snippet*** is a couple `(s, L)` where `s` is a set of ordered characters of the alphabet of a given [computer language](https://en.wikipedia.org/wiki/Computer_language) `L`.
>
> A ***valid code snippet*** is a code snippet `(s, L)` where `s` respects the vocabulary, the syntactic rules and the semantic rules of `L`.

Thereafter, by abuse of language, we will simply note `s` a code snippet `(s, L)`. It will be implicit that a code snippet refers to some computer language `L`.

**Remark**

In the definition above, the set of characters `s` is supposed to be written in only one document (a file).

> **Definition**
>
> A ***module*** is the code snippet containing all the characters of a given file.

Assuming that every computer language integrates the concept of "line break", we can give the following definition :

> **Definition**
>
> The subset of a code snippet defined by the ordered characters between two consecutive line breaks is called a ***line of code***. If the code snippet has no line break, it has only one line of code which is the code snippet itself.


> **Definition**
>
> We call **S** the couple `(S, +)` where `S` is the set of all the possible code snippets of a given language and the additional operation `+` is defined by the concatenation operation.
>
> We call call **V** the subset of `(S, +)` defined by all the possible valid code snippets of a given language.

**Remark**

The concatenation of two code snippets is a code snippet, so the operation `+` is a function from (**S** x **S**) to **S**.
```
+ : (S x S)              ->    S
    'Hello' + ' world'   =     'Hello world'
```

> **Proposition**
>
> The operation `+` is an internal operation of **V**. In other words, if `s` and `t` are two valid code snippets, then `s + t` is a valid code snippet.
>

> **Definition**
>
> We call ***system*** the triplet (H, S, D) corresponding to a functional set, where H is a hardware, S is a software, and D some data.


> **Definition [<sup>w</sup>](https://en.wikipedia.org/wiki/Information_system)**
>
> The term ***hardware*** is refers to machinery and equipment. In a modern information system, this category includes the computer itself and all of its support equipment. The support equipment includes input and output devices, storage devices and communications devices.

> **Definition [<sup>w</sup>](https://en.wikipedia.org/wiki/Information_system)**
>
> The term ***software*** refers to computer programs defined as the machine-readable instructions that direct the circuitry within the hardware parts of the system to function in ways that produce useful information from data.
>
> Thereafter, we will simply call ***program*** the set of machine-readable instructions of a given system. In other words, the program is the set of the modules of the software.

> **Definition [<sup>w</sup>](https://en.wikipedia.org/wiki/Information_system)**
>
> ***Data*** are facts that are used by systems to produce useful information. In modern information systems, data are generally stored in machine-readable form on disk until the computer needs them.

By nature, a system evolves over time as a result of the current processes running on it, and because of the eventual inputs received from out of the system.

> **Definition**
>
> A ***process*** is a couple `(l, p)` where `l` is the instruction currently executed by a processor `p`.


> **Definition**
>
> The ***state of the system*** `S` is the couple `(D, P)` where `D` represents the data of the system and `P` the set of processes running at a time `t`.



