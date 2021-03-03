# Javascript Codewars Kata Solutions

### 5 Kyu - Diophantine Equation

#### Details:  

In mathematics, a Diophantine equation is a polynomial equation, usually with two or more unknowns, such that only the integer solutions are sought or studied.

In this kata we want to find all integers x, y (x >= 0, y >= 0) solutions of a diophantine equation of the form:

x^2 - 4 * y^2 = n
(where the unknowns are x and y, and n is a given positive number) in decreasing order of the positive xi.

If there is no solution return [ ] or "[ ]" or "". (See "RUN SAMPLE TESTS" for examples of returns).

#### Solution: 

```
 function solequa (n) {

  let result = [];
  
  for(let i = 0 ; i  <= Math.trunc(Math.pow(n,1/2)); i++) {

    if(!(n % i == 0)) continue;
    
    let j = n / i;
    
    let y = (j - i) / 4;
    
    let x = i + 2 * y;
    
    Number.isInteger(x) && Number.isInteger(y) && x >= 0 && y >= 0 && i == x - 2*y && j == x + 2*y && result.push([x,y]);
  }
  
  return result;
}
  
```

### 6 Kyu - Street Fighter 2 - Character Selection

#### Details:  

Short Intro

Some of you might remember spending afternoons playing Street Fighter 2 in some Arcade back in the 90s or emulating it nowadays with the numerous emulators for retro consoles.

Can you solve this kata? Suuure-You-Can!

UPDATE: a new kata's harder version is available here.

The Kata

You'll have to simulate the video game's character selection screen behaviour, more specifically the selection grid. 

#### Solution: 

```
   function streetFighterSelection(fighters, position, moves){

    const controller = new Controller(position, [2,6]);

    return moves.map((e) => {

      const [y,x] = controller.changePosition(e);

      return fighters[y][x];

    });

  }

  function Controller(position, size) {

    [this.yMax, this.xMax] = size;

    this.xMax--;

    this.yMax--;

    [this.y, this.x] = position;

    this.dirController = {

      left: () => {

        if(this.x == 0) return [this.y, this.x = this.xMax];

        return [this.y, --this.x];
      },

      right: () => {

        if(this.x == this.xMax) return [this.y, this.x = 0];

         return [this.y, ++this.x];
      },

      up: () => {

        if(this.y > 0) this.y--;

         return [this.y, this.x];

      },

      down: () => {

        if(this.y < this.yMax) this.y++;

        return [this.y, this.x];

      }

    };


    this.changePosition = (dir) => {

      return this.dirController[dir]();

    }
  }
  
```

### 5 Kyu - MergeSort "merge" function

#### Details:  

In this excercise, we will implement the "merge" function from MergeSort.

MergeSort is often taught in Computer Science as the canonical example of the "Divide and Conquer" algorithm. The strategy of MergeSort is both simple and profound, leveraging two simple-to-prove mathematical facts (1. That every list of 1 element is "sorted" ... and 2. It is much easier to combine two already-sorted lists into 1 sorted list than it is to sort a big list all at once) to yield an algorithm with a worst-case complexity of O(n log n).

Basically, MergeSort works like this:

If we get a list of size 1, then it's already sorted: we're done. Just return that value.
Otherwise; break the list you have to sort in half: 2a. MergeSort the first half. 2b. MergeSort the second half. 2c. "Merge" the two sorted lists for 2a and 2b together. Voila: sorted.
2c is where the MergeSort "merge" function comes in. It takes two already-sorted lists (arrays, in this example) and returns one large sorted list.

The name of the function in this example is "mergesorted". It should return a big sorted array from two smaller sorted arrays: e.g.

mergesorted([1,2],[3,4]) //should: [1,2,3,4]

mergesorted([1,2],[3]) //should: [1,2,3]

mergesorted([1],[2, 3]) //should: [1,2,3]

#### Solution: 

```
   function mergesorted(a, b) {
  
    if(a[a.length - 1] <= b[b.length - 1]) return sortMerge(a, b);
    return sortMerge(b, a);
  
    }

  function sortMerge(a, b) {

    a.forEach((e, i) => {
      let index = b.findIndex((o) => e <= o);
      b.splice(index, 0, e);
    });

    return b;
  }

```

### 5 Kyu - Tail recursion with trampoline

#### Details:  

Functional programming prefers recursion over iteration.

Recursive functions are often more readable than its iterative version.

Besides, functional programming avoids declaring variables, so functions do not have mutable state. Recursion can solve problems without mutable state.

*More...*

#### Solution: 

```
  function thunk(fn, ...args) {
    return function () {
      return fn.call(null, ...args);
    }
  }

  function trampoline(thunk) {

    let result = thunk();

    while (typeof result === 'function') {
       result = result();
    }

    return result;

  }

  function even(n) {
      if(n === 0) {
        return true;
      } else {
        return thunk(odd, n - 1)
      }
    }

  function odd(n) {
      if(n === 0) {
        return false;
      } else {
        return thunk(even, n - 1)
      }
    }

  function isEven(n) {

    return trampoline(thunk(even, n));
  }

  function isOdd(n) {
    return trampoline(thunk(odd, n));
  }

```

### 5 Kyu - Using closures to share class state

#### Details:  

In object-oriented programming, it is sometimes useful to have private shared state among all instances of a class; in other languages, like ruby, this shared state would be tracked with a class variable. In javascript we achieve this through closures and immediately-invoked function expressions.

In this kata, I want you to write make a Cat constructor that takes arguments name and weight to instantiate a new cat object. The constructor should also have an averageWeight method that returns the average weight of cats created with the constructor.

#### Solution: 

```
   var Cat = (function () {

    var mapWeight = new Map();

    function CatClass (name, weight) {

      if(arguments.length <= 1) throw "Error";

      this._weight = weight;
      this._name = name;
      mapWeight.set(this._name, this._weight);

      Object.defineProperty(this, 'weight', {
        set: function (x) { 
          this._weight = x;
          mapWeight.set(this._name, this._weight);
        },
        get: function() {
          return this._weight;
        }
      });

      Object.defineProperty(this, 'name', {
            set: function (x) { 
              this._name = x;
            },
            get: function() {
              return this._name;
            }
          });
    }

    CatClass.averageWeight = function () {

        return Array.from(mapWeight.values()).reduce((sum, e) => sum + e, 0) / mapWeight.size;

      }

    return CatClass;

  }());

```

### 4 Kyu - Dependency Injection

#### Details:  

Did you hear about Dependency Injection pattern? The main idea of this pattern is that you may have ability to pass dependencies into your function in any order and they will be resolved automatically. Take a look at this:

```
  var myDependentFunc = inject(function (secondDepency, firstDependency) {
    firstDependency();
    secondDepency();
  });

  myDependentFunc();
```

As you can see we just put some variables into the function's signature and work with them as usualy. But we know nothing about where these variables are located! Let's assume that all dependencies are stored in the single hash object (for instanse 'deps') and the injector function will be sought among 'deps' properties:

```
  var deps = {
    'firstDependency': function () {return 'this is firstDependency';},
    'secondDepency': function () {return 'this is secondDepency';},
  };
```

Ok, I hope this is clear. Also, in order to setup DependencyInjector (DI) we need to specify dependency object:

```
  var DI = function (dependency) {
    this.dependency = dependency;
  };
```

Your task is create DI.prototype.inject method that will return a new function with resolved dependencies. And don't forget about nested functions. You shouldn't handle them.

#### Solution: 

```
   var DI = function (dependency) {
    this.dependency = dependency;
  };
  
  DI.prototype.inject = function (func) {

    if(func.length > 0) {
      let funcString = func.toString();
      let parameterNameList = funcString.slice(funcString.indexOf('(') + 1, funcString.indexOf(')')).split(',');
      parameterNameList.forEach(s => {
        s = s.trim();
        func = func.bind(this, this.dependency[s]);
      });
    }

    return func;
    
  }
```
