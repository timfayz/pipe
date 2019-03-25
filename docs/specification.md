# pipe Language Specification

This document describes semantic core and syntax of the language. It includes grammar rules, reserved keywords, predefined types, functions, data and execution model, formatting options, minimum set of functionality and high-level language overview. This specification should be *sufficient* developer to implement its compiler or interpreter for a given platform. 

**Work in progress..**

1. Introduction (high-level overview)
   1. Semantic review (intro to semantic core)
   2. Features review (minimal set of features)
   3. Syntax review (intro to physical representation)
   4. How to read Specification
2. Mental model (metal shift)
   1. Turing, stack machine & CPU
   2. Programming paradigms
   3. Types
      1. static vs dynamic
      2. build-in vs predefined
   4. Object, class, unit, container ...
   5. Function, procedure, method ...
   6. Encapsulation
   7. Inheritance and polymorphism
   8. Interface and protocol
   9.  References and values
   10. Concurrency 
   11. Exceptions
   12. Garbage collector
   13. Tests and verification
   14. Module, package, file
3. Semantic model
   1. Memory model
   2. Data model
      1. Types
      2. Define, assign, access
   3. Execution model
      1. Control flow
      2. Multiple results
      3. Variable arguments
      4. Default values
      5. Invocation or call
      6. Evaluation order
      7. Parallel execution
      8. Invariants, pre-/post-conditions
      9. Garbage collector
4. Syntax and grammar
   1. Compilation units
   2. Lexeme categories
      1. Types
      2. Values
      3. Expressions
   3. Text
      1. Expression vs statements
      2. Definition vs assignments
   4. Comments
   5. Separators
   6. Predefined operators
      1. Logic operators
      2. Math operators
      3. Precedence table
5. Implementation
   1. Architecture 
   2. Recommendations

<!--
C++ 3 catagories of language entities:
1. object declarations 
2. expressions and operators
3. types
-->