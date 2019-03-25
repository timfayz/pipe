# pipe

> If there is *intermediate representation* for machines, there should be something for *humans*..

```
Human = :{                                  -- new type
    Name :str
    age :int                                -- private field
    Parents :*Human[2]                      -- ancestor tree
}

:Human.Introduce () =                       -- public "method"
    stdout.print "Hi! I'm ", .Name          

:Human.HowOld () :int =                     -- age "getter"
    ret .age
```
```
fibonacci (n :int) :int =                   -- Fibonacci sequence
    if n == 0
        ret 0
    ret .(n - 1) + n
```
```
fibonacci (0) => 0                          -- recursive paradise

fibonacci (n) => .(n - 1) + n
```
```
<ul>                                        <!-- code embedding -->
@{for i := 5, i--}        
    <li>$i</li>
</ul>
```
[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/timfayz/pipe?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)



## Abstract

**pipe** is a *research proposal* to create conceptual programming language that draw narrow line among many PLs, DSLs and even declarative notations to form generalized *semantic core* that will be sufficient to express different programming techniques, paradigms and human intentions. pipe do not follow an approach to include *every* feature from XYZ languages. On the contrary, simple core but *expressible syntax* is what pipe strives for. The less complexity we bring to its core, the more complex software we will build upon. 



## Get started

1. [Feature overview](docs/features.md)
2. [Comparison with other languages](docs/comparison.md)
3. [Transfer natural language to pipe](docs/natural-language.md)
4. [Language Specification](docs/specification.md)
5. [Proposed architecture](docs/architecture.md)
6. [References](docs/references.md)


## Why "pipe"?

Real pipes have a good association with *medium* for a flow. What kind of flow you decide. It might be a character stream between processes, real water flow controlled by a software or just a though flow laid out on your code. Our task is to give you right fittings, high quality materials, different gauges for different purposes and do not *impede* building your own pipework. 



## Contacts
If you have questions, feel free to write me a message (tim.fayzrakhmanov@gmail.com) or open an [issue](https://github.com/timfayz/pipe-lang/issues).