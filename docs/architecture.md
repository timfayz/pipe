# Architecture

```nomnoml
#font: mono
#fontSize: 10
#edges: hard
#stroke: #111
#fill: #fff; 
#lineWidth: 2
#padding: 10
#spacing: 30

[pipe]->[LLVM]
[pipe]->[Webassembly]
[pipe]->[Python]
```