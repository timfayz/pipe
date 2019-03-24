# Feature overview
Many of pipe features are quite unique and an abstract description alone hardly give you a hint. That's why every item feeded with sample code and practical considerations.

### Quick jumps
1. Rethink programming notation
2. [Meta-programming & Self-modifiable code]()
3. [Reflection and Semantic search]()
4. [SQL as part of the language]()
5. [In-code shell]()
6. [Code embedding]()
7. [Pre, post-conditions and invariants]()
8. [Optional types]()
9. First-class
10. Interface

## Rethink programming notation
pipe tries to gather best practices and give innovative view how modern programming language should look like. No semicolons, no tabular spaces, no structs, no classes, optional curly brackets and build-in (re)formatting. 

pipe is a balance b/w modern "sleekness" and time-proofed techniques that served us making less keystrokes, distinguish structure and write well-formed code.

### Static / dynamic types
```
name :str = "Timur"               -- explicit types
pi := 3.14                        -- auto type detection
x = 0                             -- dynamic types (expression-oriented programming)
x = (1, false, "hello", 3.14)     -- no error
```
### Simple run-time reflection
```
print %x.Type == :untyped         -- true
print (%x .Type, .Name)           -- ":untyped x"
```
### Contexted multi-line treatment
```
names :str[] =                    -- multiline assignment
  "John"
  "Robert"
  "Tim"
                                  -- unevaluated raw string
title :str = `
  These are my
    Lieblings Friends!
`
print 
  title 
  names..                         -- unfold `names` and print each item
```
### Concise encapsulation
Identifier should carry meaning! Now is it constant or variable, "private" or "protected" is derived from name.
```
CONS  := 256                      -- exported constant  
_CONS := 1024                     -- unexported constant
Var   := "Hello"                  -- exported variable
var   := "World"                  -- unexported variable
                                  -- the same naming rules apply for all types of labels
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
### Function, procedure or transition?
```
                                  -- or
  .IsObsolete () :bool = {
    ret .age > 100
  }            
                                  -- or
  .IsObsolete () :bool => .age > 100
```
### Compound types + named fields = ?
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

Humanoid = :{                     -- type composition
  :Robot                          -- "squash" or unfold type members here
  :Human                          -- despite being squashed, explicit path always preserved  
  age :int
  Name :str 
}

me :Humanoid =                    -- create new :Humanoid
  .Name = "Arnold"
  .Blood = true 
                                  -- other fields initialized with 0/nulls

me.Robot.Speak()                  -- "I am 0"
me.Human.Speak()                  -- "My name is Arnold"
me.Speak()                        -- "My name is Arnold"
                                  -- order matters, :Human "overloading precedence" is higher
                                  -- when ambiguous just use explicit path
```
### Type casting
```
x = 1
y :int = :int(x)
-- Hm... What if I want to check whether it can be casted or not? Otherwise, just set it to 0
z :int = :int(x) == :int ? x : 0  -- solution
```
### Interfaces?
In pipe there is no separate notion for **interface**. Instead, simple check if type *comply* to other type during the casting serve as a technique to generalize different concepts about the same thing.
```
IHumanoid = :{
  Speak ()
  Blood :bool | Model :int
}

if :IHumanoid(me)                 -- check type compliance
  print "I'm either Human or Robot!"
```
### Default type values
It might be strange but types (excerpt build-in ones) can have default values. 
```
myInt = :int 
:myInt = 10

x :myInt
print x                           -- "10"
```

### Where is main() BTW?
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

## Homogeneous type system
There is no difference between build-in types or user-defined all types follow and defined under the same rules. The only difference is that primitive types are well optimized for hardware and always be used during optimization stage when possible. However, to distinguish build-in types from user-defined pipe made a little exception - they are lowercase despite being "imported" from stdlib. It is forbidden in normal cases.

## Reflection


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
pipe introduces **window**s. Using `@{...}` you can inject logic right into the text. File format doesn't matter. You can include other files, import libraries, apply control flow, I/O and all other functionality available in normal code.

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
Optionally, pipe can automatically hide/unhide its "presence" by commenting out all its windows and identifiers used across the file:
```bash
pipe --injected index.p.html --hide index.html
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
pipe --injected index.p.html index.html
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
What about pipe files itself? The same! But only *one level* of nesting. This is proposed answer for all sorts of "meta-programming" and preprocessing features.

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