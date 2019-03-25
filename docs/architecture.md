# pipe Architecture
[Return to the beginning](/README.md#get-started)

**Work in progress..**

<!--
```nomnoml
#font: mono
#fontSize: 10
#edges: hard
#stroke: #111
#fill: #fff; 
#lineWidth: 2
#padding: 10
#spacing: 30

[<frame>pipe sources
|text files
|graphical (UML)
|in-code snippets
]->[front-end]


[front-end]->[semantic core]
[semantic core]<->[intermediate representation|optimizations]
[intermediate representation]->[code generations]

[code generations]->[back-ends]

[<class>back-ends|
LLVM|
Webassembly|
Java bytecode|
HTML/XML|
...
]

[intermediate representation]->[VM/Interpreter]
[semantic core]->[Visualizer]
[semantic core]->[Static analyzer]
```
-->
![](/docs/diagrams/architecture.png)