# pipe Overview
[Return to the beginning](/README.md#get-started)

Every feature and concept pipe introduces might be unique and just an abstract description alone hardly give you a hint. That's why every item of this document is feeded with a sample code how one would *express* it by a code or *use* it under CLI. Under every title there might a tag list which points to common synonyms and programming concepts the language is going to cover. This document doesn't distinguish what is considered particular *feature* or *concept* because every new concept can be considered as a feature and vice versa. Just go along the text and examples.

<!--
### Quick jump
1. Rethink programming notation
2. [Code embedding or self-modifiable code]()
3. [Reflection]()
4. [Semantic search]()
5. [SQL as part of the language]()
6. [In-code shell]()
7. [Pre, post-conditions and invariants]()
8. [Optional types]()
9.  First-class X
10. Interfaces
11. Actor model
12. Access to intrinsic properties
13. In-code translation for learning
-->

## Rethink programming notation
**pipe** tries to gather best practices and give innovative view how modern programming language might look like. 

**pipe** is a balance between modern "sleekness" and time-proofed techniques that still serve us making less keystrokes, distinguish structure and write well-formed code.

**pipe** strives to eliminate ambiguous interpretations, [overchoice phenomenon](https://en.wikipedia.org/wiki/Overchoice) and contradictions between *visible* code flow and *implied* semantics.

**pipe** is an attempt to create *semantic core* such that its vital features, internal AST, "supported" models and syntax options can become an [independent](https://en.wikipedia.org/wiki/Language-agnostic) layer for further self-generation into existing languages, back-ends and platforms.



## Types. Redefined
pipe takes an approach that **_everything has a type_** and **_type itself is a type in it's own name_**. Types are central point of pipe system to solve many programming problems. It includes generics, type extension and inheritance, type conformance, optional typing and many more. In the next sections you will see practical examples and notions that pipe's typing system trying to cover.


### Dynamic vs static
<sup>strict typing, dynamic typing, type inference, optional typing</sup>

pipe can be both - strictly typed language when type explicitly/implicitly defined and fully dynamic when any notion of type is omited. Underlying implementation however always assign a type to any identifier it meets. If something doesn't seem to have a type, it is actually assigned as a type of `:untyped`. 

Automatic type inference achieved by using a colon `:` to omit a name and infer it at compile time. 

Dynamic identifier (or `:untyped`) can be created by assigning `=` to non-existent identifier. 
```
name :str = "Timur"               -- explicit type
pi := 3.14                        -- auto type inference
x = 0                             -- dynamic type (expression-oriented programming)
x = (1, false, "hello", 3.14)     -- no error
pi = 3                            -- error
name = 't'                        -- error
```

### Homogeneous type system
There is no difference between build-in types or user-defined all types follow and defined under the same rules. The only difference is that primitive types are well optimized for hardware and always be used during optimization stage when possible. However, to distinguish build-in types from user-defined, pipe made a little exception - they are lowercase despite being "imported" from stdlib which is forbidden in normal cases.

### Constraint vs interface vs protocol ..
<sup>contract-based programming, type constraints, protocols</sup>

pipe distinguish no difference among interfaces to conform certain type's behavior, nor constraint to be sure some type's properties are hold, nor protocols or contracts that basically the same as previous.
```
:constraint[T] =
```

### Interfaces
<sup>merge to above</sup>

In pipe there is no separate notion for **interface**. Instead, simple check if type *complies* to other type during casting or argument passing serve as a technique to generalize different concepts about the same thing.
```
IHumanoid = :{                    -- or Humanoider if you like
  Speak ()
  Blood :bool | Model :int
}

if :IHumanoid(me)                 -- check type compliance
  print "Yes! I don't know if I'm Human or Robot!"

Sayer (:IHumanoid h) = h.Speak()
Sayer(me)                         -- "My name is Arnold", see previous section
```

### Casting
Type casting as simple as that:
```
x = 1
y :int = :int(x)
-- Hm... What if I want to check whether it can be casted or not? Otherwise, just set it to 0
z :int = :int(x) == :int ? x : 0  -- solution
```

### Reflection
<sup>compile and run-time reflection, meta programming, introspection, indirect invocation</sup>

pipe uses `%` symbol to reflect identifier and access its properties or "meta" information.
```
print %x.type == :untyped         -- true
print (%x .type, .name)           -- ":untyped x"
```

### Contexted multi-line treatment
```
names :str[] =                    -- multiline assignment
  "John"
  "Robert"
  "Tim"
                                  -- multiline raw string assignment
title :str = `
  These are my
    Lieblings Friends!
`
print                             -- multiline argument passing
  title 
  names..                         -- unfold `names` and print each item
```

### Identifier names carry meaning

pipes tries to infer as much information as possible from every character and position in your code in order to minify keystrokes. If so identifier should carry meaning! The identifier properties such as constant or variable, "private" or "protected" are derived from its name.
```
CONS  := 256                      -- exported constant (cannot be less than 2 characters)
_CONS := 1024                     -- unexported constant
Var   := "Hello"                  -- exported variable
var   := "World"                  -- unexported variable
                                  -- the same naming rules apply to all types of identifiers
```

### Group assignment
```
i, j, k := 1                      
a, b := 2, 3
x := y := 4 

print i, j, k, a, b, x, y         -- "1 1 1 2 3 4 4"
```

### Static, multidimensional and dynamic arrays
```
                                      -- array initialization
slice1D := (1,2,3,4)                  -- dynamic array, "list", "set" or "slice"
arr1D :int[4]       = 1..4            -- (1,2,3,4)
arr2D :int[4][4]    = 1..4.1..4       -- ((1,2,3,4),(1,2,3,4),..)
arr3D :int[4][4][4] = 1{4}.1{2}.1{4}  -- fill first half of 3D cube (X.Y.Z) with 1s

                                  -- accessing array elements
arr1D[-1]                         -- last, -2 penult, etc
arr1D[:]                          -- all 
arr1D..                           -- all (unfold)
arr1D[2:4]                        -- range
arr1D[1,4]                        -- selected
arr3D[1][2][3]                    -- nested selection (classic)
```

### Uniform Function Call (UFC)
```                                  
sum (a, b :int) :int => a + b
sum(5, 5)                         -- "10", standard
5 sum 5                           -- "10", infix
5.sum(5)                          -- "10", carrying
sum 5, 5                          -- "10", prefix (no parenthesis)

                                  -- uniform data attributes access
obj = :{p1, p2} = (1, 2)
print(obj .p1, .p2)               -- "1, 2"
print(obj.p1, obj.p2)             -- "1, 2"
print obj> .p1 add .p2            -- "3" (namespace carrying)
```

### () equals to function, procedure, lambda, ..
<sup>procedure, transition, function, lambda function</sup>

```
-- WIP
                                  -- draft 1
funcName () :bool = {
  ret 1 > 0
}
funcName () :bool =
  ret 1 > 0          

                                  -- draft 2
funcName () :bool => 1 > 0

                                  -- draft 3
funcName := (:int) -> :int [
  body
]
funcName := :int -> . + 10
```

<!--
### Recursive paradise
```
WIP
```
-->

### Compound types + named fields = X
Want to create struct, class, container, unit, records or just a structure with named fields? There is no name for this anymore. Just use concept of **compound types** and **named fields**
```
Human = :{                        
  Blood :bool                 
  Parents :*Human[2]              -- 2 length array of :Human's type pointers/references
}
                                  -- now `:Human.` is carrying
  .Speak () =                     -- define :Human's Speak() method by value
    print "My name is ", .Name

Robot = :{                   
  Model :int
  Manufacturer :str
}
  .Speak () =                     
    print "I am ", .Model

  .IsObsolete () :bool =             
    ret .age > 100

Humanoid = :{                     -- compound type
  :Robot                          -- type embedding or squash/unfold type members 
  :Human                          -- despite embedding, explicit path always preserved  
  age :int
  Name :str 
}

me :Humanoid =                    -- create new :Humanoid
  .Name = "Arnold"
  .Blood = true 
                                  -- other fields initialized with 0/nulls

me:Robot.Speak()                  -- "I am 0"
me:Human.Speak()                  -- "My name is Arnold"
me.Speak()                        -- "My name is Arnold"
                                  -- order matters, :Human "overriding precedence" is higher
                                  -- when ambiguous just use explicit path (experimental)
```

### Overloading and overriding
Just to recap: **overloading** means 2 methods with the same name and different signatures (including return value); **overriding** means 2 methods with the same name and signature but different body.
```
-- Overloading
plus (a, b :int)
plus (a, b :str)
plus (a, b :float) =              -- should be self-explanatory
  ret a + b

-- Overriding (1) direct
minus (a, b :int) => a - b 
minus (a, b :int) => a + b        -- error

-- Overriding (2) through inheritance
Vector = :int[2]                  -- define type

:Vector.add (:Vector v) =         -- add `add` method
  .[0] += v[0]                    
  .[1] += v[1]

AVector = :{                      -- define new annotated vector
  :Vector
  counter :int
}

:AVector.add (:AVector v) =
  .:Vector.add(:Vector(v))         -- type casting
  .counter++
```
As you can see it is not real "overriding" rather than method hiding. You *always* has an access to inherited methods through explicit path. In our case: `:AVector:Vector.add()`


### Default type values
It might be strange but types (excerpt build-in ones) can have default values. 
```
myInt = :int 
:myInt = 10

x :myInt
print x                           -- "10"
```

### Where is main() by the way?
Optional, unless one wants it to define *explicitly*
```
import pipe/io

main (argc :int, argv :*str[]) =
  if argc < 3
  io.stderr.print 
    "Error: incorrect number of arguments"
    "Passed ", argc, ", expected 3"
  exit 0
```

## First-class X
```
```
## Contract based programming
Run-time verification might be an important concern for mission-critical software systems, where performance is not vital. At the moment pipe do not have special construction for this. Simply because ... Here is how pre/post-condition and invariants can be expressed.
```
myContract = :{     -- define type and assign its fields as default values
  pre :block
  inv :block
  post :block
} =
  .pre = 
    if a < 0 && b < 0
      ret -1
  
  .post =
    if sum > 100
      ret -1

  .inv =
    if a + b < 100
      ret -1


strictSum (a, b :int) :int = 
  myContract.pre()
  defer myContract.post()         -- execute right before return (will run after .inv)
  myContract.inv() >              -- start executing .inv right before every line
                                  -- you can change sign to < and it will run after
    sum = a + b
    a -= 10
    b -= 10
    ret sum

```

## Symbolic computation
<sup>symbolic mathematics, algebraic computations</sup>

pipe proposes simple mechanism for converting mathematical expressions back and forth between LaTeX math notation and pipe's math expressions.


## Lisp rebirth
Do you remember the magic of Lisp? Its simple syntax and number of primitives still cause people feel of adoration and rumors that anyone who enters Computer Science *must* learn it at least once. Indeed Lisp's philosophy is hardly exhaustive but what happens inside is simply *Stack machine* + *Polish prefix notation*. pipe found both suitable for backing internal AST logic and express semantic core. It makes transfer to existing infrastructure of back-ends, hardware platforms and VMs much easier. Thus, while you write pipe code, you can think of it as *syntactic sugar* on top of polish notation to simplify verbosity and facilitate your mental habits.
```
import pipe/ast

arr :int[] = 1..5
                                  -- the same as
ast.Import `
(assign 
  (label arr2 (:slice int{10}))
  1 2 3 4 5
`.Run()

plus (a, b :int) :int =
  ret a + b
                                  -- the same as
ast.Import `
(assign 
  (label plus2 (:func a :int b :int (return :int)))
  '(ret add(a b))
)
`.Run()
```
pipe highly discourage mixing both syntaxes under one roof. That's why it will require  either additional steps or explicit flag to use.



## Code analysis 
pipe's answer to emerging demand for static code analysis is the following: **reflection** + **queries** = **code analysis**. Standard library includes simple API for generating, parsing and querying meta data from and to execution environments. Technically speaking, you can import annotated AST from code snippets, programs and even diagrams, validate it and export back to supported media. Having an access to AST as a "first-class" data gives you a whole new horizon of opportunities. You can literally build execution environment "on the fly" or send it as serialized object to other environments.

```
import 
  pipe/ast                    -- stdlib for manipulating pipe AST
  pipe/io .                   -- squash `io.` namespace and eliminate prefixing
  pipe/ql                     -- build-in query language

src := `                      -- source can be any (file, socket, literal string)
plus (a, b :int) :int =
  ret a + b

minus (a, b :int) :int =
  ret a - b

pow (a :int) =
  ret a*a
`

program := ast.Import(src)    -- convert snippet into "importable" program

if !ast.Validate(program) 
  exit

ast.Import(program, .env)     -- inject into current execution environment
stdout.print(plus 2 2)        -- now we can apply one of the function

result :=                     -- let's find functions that has more that 2 arguments
  ql.>                        -- carry namespace (ql.) per line
    Select ast.T_FUNC 
    From program
    When (%f) => f.Sign.ArgsNum > 1

stdout.print(result.. .Sign)  -- unfold array and append .Sign per each item
                              -- "plus (a, b :int) :int"
                              -- "minus (a, b :int) :int"
```



## Code embedding
pipe introduces **windows**. Using `@{...}` you can inject logic right into the text. File format doesn't matter. You can include files, import libs, apply control flow, I/O and all other functionality available in normal code but just withing the windows.

```html
<!--index.p.html-->
@{
  title := "My favorite colors"
  days := ("Green", "Blue", "White", "Black")
}
<title>$title</title>
<body>
  <ul>
  @{for day := days..}
    <li>$day color</li>
  </ul>
</body>
```
Optionally, pipe can automatically hide/unhide its "presence" by commenting out its windows and identifiers used across the file:
```bash
pipe pre --hide index.p.html index.html
```
```html
<!--@{
  title := "My favorite colors"
  days := ("Green", "Blue", "White", "Black")
}-->
<title><!--$title--></title>
<body>
  <ul>
  <!--@{for day := days..}-->
    <li><!--$day--> color</li>
  </ul>
</body>
```
```
pipe pre index.p.html index.html
```
```html
<title>My favorite colors</title>
<body>
  <ul>
    <li>Green color</li>
    <li>Blue color</li>
    <li>White color</li>
    <li>Black color</li>
  </ul>
</body>
```
What about pipe files itself? The same! But only *one level* of nesting as with other files. This is proposed answer for all sorts of "meta-programming", "generative programming" and preprocessing features. pipe see no difference b/w "preprocessing language" and standard one.
```
-- main.p

@{
  importList := ("io", "ast", "json")
  for v := importList..
}
    <<<0                          -- return indentation of affected sub-block back to 0 level
    import pipe/$v

imported := $%importList.len      -- reflect list to get its "meta" length
print imported
```
```
pipe pre main.p
```
```
-- main.p

import pipe/io
import pipe/ast
import pipe/json

imported := 3      -- reflect list to get its "meta" length
print imported
```

### Quine
```
example of producing a copy of its own source 
```
<!--
## What one's language should support

* Do not contradict the natural human/programmer thinking
* Parallel programming (SCOOP)
* Meta-programming / Macros / Templates / scripting abilities
* Reflection and code generation
* Formal specification (contract-based design?)
* Support different types of programming paradigms (OOP, functional, visual, module, etc)
* Intuitive syntax
* Hardware neutral memory management
* Partial compilation
* Self-compilation
* Language extension
* Dead code elimination
* Integration with existing languages (?)
* Relation algebra (SQL)
* Static structure description (HTML)
* JIT compilation
* Interactive shell
* Fast DSL generation (Macros)
* Language toolchain
* Analyze program without running them
* Lexical scoping (different languages over API)
* Parse LaTeX math expressions into valid code that can be evaluated 
* Support for your best paradigm
  * Functional
  * Message passing
  * Object-Oriented (Class-based)
  * Prototype
* Ideomatic
  * One ideomatic way over a lot of choices for the *same* thing:
    - a = 2, 2 = a, (assign 2 a); 
    - No! Just: a := 2
  - (reasoning) 
    - The Paradox of Choice - the more choices, less happiness. 
    - *less is more*
    - When there is no one way of doing one thing, it happens to arise ambiguity among different code and people
* Build-in code formatting

## Feature "attributes"
Have you ever played Video games like ... Every characters has it's own pros and cons in the view of a table or chart. pipe takes similar approach by introducing "syntax attributes". List:
1. Strictness 
2. Simplicity (Expressiveness)
3. Shortness
4. Slickness
-->