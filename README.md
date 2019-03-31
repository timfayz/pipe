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
    if n == 0                               -- classic way
        ret 0
    ret .(n - 1) + n
                                            
fibonacci (n) => .(n - 1) + n               -- Fibonacci sequence
fibonacci (0) => 0                          -- with function accepting literals
```
```
<ul>                                        <!-- embedded code -->
@{for i := 5, i > 0, i--}        
    <li>$i</li>
</ul>
```

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/timfayz/pipe?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)



## Abstract

**pipe** is a *research proposal* to create conceptual programming language that draw narrow line among many PLs, DSLs and even declarative notations to form generalized *semantic core* that will be sufficient to express different programming techniques, paradigms and human intentions. pipe do not follow an approach to include *every* feature from XYZ languages. On the contrary, *simple core* but *expressible syntax* is what pipe strives for. The less complexity in its core, the more complex and reliable software you'll build upon. 

<!--
pipe's main concern is to protect developer's time investments into learning every new particular language. 

## Rationale

The era of emerging computer systems in 60-70s gave a whole new horizon for engineers and researches to think about how human will interact with the computers. The "programming" in its classic form we know it today wasn't existed yet so many people had no idea what it should be and created totally new and unexpected ways of interacting with the computers. Sometimes it was still just a binary hand-written code and sometimes it was a magic visual drawing using stylus and tablet. Both extremes (and actually many others) failed in its success to become a mainstream. Some recognizable researchers still believe that in 10 or 40 years we will interact and mainly *program* computers with our voice, gestures or spacial capabilities by drawing. However, through the years of exploring how we live, what we consume and how we interact with each other gave a clear answer what programming will be in forseeable future. And the answer lays in ordinary books or our deep-rooted ability to write ideas on a paper. Once we have a books on our shelves (including virtual ones) we *will* code using letters since this is the only way to express things that have no visual, no spacial, no physical representation. According to this insight and years of analyzing different notations this project concludes a vector. Since we posses such a great amount of information and interdisciplinary experience, it's a right time to 
-->

## Get started

1. [pipe Overview](docs/features.md)
2. [Comparison with other languages](docs/comparison.md)
3. [Transfer natural language to pipe](docs/natural-language.md)
4. [Language Specification](docs/specification.md)
5. [Proposed architecture](docs/architecture.md)
6. [References](docs/references.md)


## Why "pipe"?

Real pipes have a good association with *medium* for a flow. What kind of flow you decide. It might be a character stream between processes, real water flow controlled by a software or just a though flow laid out on your code. Our task is to give you right fittings, high quality materials, different gauges for different purposes and do not *impede* building your own pipework. 



## Contacts
If you have any questions feel free to write me a message (tim.fayzrakhmanov@gmail.com) or open an [issue](https://github.com/timfayz/pipe-lang/issues).