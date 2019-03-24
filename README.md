# pipe

> If there is *intermediate representation* (IR) for machines, there should be something for the *humans*..

```
Human = :{                                  -- new type definition
    Name :str
    age :int                                -- private field
    Parents :*Human[2]                      -- link to ancestors
}

:Human.Introduce () =                        -- public method
    stdout.print "Hi! I'm ", .Name          

:Human.HowOld () :int =                      -- age "getter"
    ret .age
```
```
fibonacci (n :int) :int =                   -- return Fibonacci sequence
    if n == 0
        ret 0
    ret .(n - 1) + n
```

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/timfayz/pipe?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

## Abstract
**pipe** is a *research proposal* to create conceptual programming language that is sufficient to become Intermediate Representation (IR) for human thoughts. Despite being a research project pipe strives to be as *pragmatic* as possible. It is an attempt to distinguish narrow line among different programming languages, DSLs and even declarative notations to form generalized *semantic core* that will be sufficient to further interpolate as *Human* Intermediate Representation (HIR).



## Historical background
Design and comprehension of programming language is a key to understand why there is hardware *in the first place*.

## Proposed Solution

...

## Get started

1. [Feature overview](docs/features.md)
2. [Comparison with other languages](docs/comparison.md)
3. [Transfer natural language to pipe](docs/natlang-to-pipe.md)
4. [Language Specification](docs/specification.md)
5. [Proposed architecture](docs/architecture.md)
6. [References](docs/references.md)

## Why "pipe"?
The notion of pipe fits good to philosophy of the project. Pipes are used as a *medium* for a flow. It can be character flow in Unix, thought flow of human, water flow in houses, electricity in mains and a light flow in Ethernet cables. Our task is to give you right fittings for the right ports, use high quality materials, provide different gauges for different purposes and do not *impede* your imagination of creating your own pipework!

## Contacts
If you have *any* questions, feel free to write me a message (tim.fayzrakhmanov@gmail.com) or open an [issue](https://github.com/timfayz/pipe-lang/issues).