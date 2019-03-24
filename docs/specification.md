# The pipe Language Specification

This document describes core semantics and syntax of the language. It includes syntax, grammar rules, reserved keywords, predefined types, predefined functions, semantics, data and execution model, formatting, minimum set of functionality and high-level overview of the language. This specification should be *sufficient* a developer to implement its compiler or interpreter for desired platform. 

1. [Introduction]() (high-level overview)
   1. Semantic review (intro to semantic core)
   2. Features review (minimal set of features)
   3. Syntax review (intro to physical representation)
   4. How to read Specification
      1. Synonyms
2. Mental model (for humans)
   1. Turing machine, CPU
   2. Programming paradigms
   3. Types
      1. static vs dynamic
      2. build-in vs predefined
   4. Object, class, unit, container ...
   5. Function, procedure, method ...
   6. Encapsulation
   7. Inheritance & Polymorphism
   8. Interface / protocol
   9.  References vs values
   10. Concurrency 
   11. Exceptions
   12. Garbage collector
   13. Testing
   14. Module, package, file
3. [Semantic model]()
   1. Memory model
   2. Data model
      1. Types
      2. Define, assign, access
   3. Execution model
      1. Control flow
      2. Multiple results
      3. Variable arguments
      4. Default values
      5. Invocation / call
      6. Evaluation order
      7. Parallel execution
      8. Invariants, pre-/post-conditions
      9. Garbage collector
4. [Syntax grammar]()
   1. Source files
   2. Text / code
      1. Expression vs statements
      2. Definition vs assignments
   3. Comments
   4. Separators
   5. Lexeme categories (?)
   6. Predefined operators
      1. Logic
      2. Math
      3. Precedence
   7. 