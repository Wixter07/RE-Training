# Week 4
## Tasks

We'll be learning about a very important theorem solver which can be crafted for different use cases. Z3 is a theorem prover from Microsoft Research. It is best used as a component in the context of other tools that require solving logical formulas over one or more theories.

You can install it using `pip install z3-solver` 


Z3 Can be used in solving ctf challenges which involves solving arithmetic equations that can't be solved manually.

### Basic solve
To solve most reversing challenges involving solving equations, it involves few concepts which might be new to you.

Lets begin with a simple solving of equations

```py
x+2*y=3
3*x-y=2
```
The first step is initialization of variables x and y
```py
x=Int('x')
y=Int('y')
```

Then we create a general purpose solver s.
`py
s=Solver()
`

Adds a constraint to a Solver s which we can get from the binary.
```py
s.add(x + 2*y==3)
s.add(3*x - y==2)
```
Next we need to checks if the solution exists for the given equation It Returns sat if the solution exist, else if, the solver cannot find a satisfying assignment, then it will return unsat
```py
s.check()
```
Then Get the satisfying assignment, which will only work if s.check() gives sat
```py
s.model()
```

A sample program looks like this.

```py
from z3 import *
x=Int('x')
y=Int('y')
s=Solver()    
s.add(x + 2*y==3)
s.add(3*x - y==2)
s.check()
while(s.check()==sat):
    print(s.model()[x])
    print(s.model()[y])
```

To create bit-vector variables and constants. The function BitVec('x', 32) creates a bit-vector variable in Z3 named x with 32 bits.

```py
x = BitVec('x', 32)
y = BitVec('y', 32)
```

Few Boolean instructions:-
1) Or() - Asserts at least one argument given is true.
2) Distinct() - Asserts that all given variables are distinct.
3) Sum() - Creates a variable which is equal to the sum of the arguments.
4) Product() - Creates a variable equal to the product of the arguments.
5) And() - Asserts that all arguments given are true.

```py
from z3 import *
x = Bool("x")
y = Bool("y")
x_or_y = Or([x,y])
x_and_y = And([x,y])
s = Solver() # create a solver s
s.add(x_or_y) # add the clause: x or y
s.check()
s.model()
```


Look into more about Z3 [here](https://z3prover.github.io/papers/programmingz3.html)
