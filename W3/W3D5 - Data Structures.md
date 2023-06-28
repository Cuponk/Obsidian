
## Abstract Data Types vs. Data Structures

* `Abstract Data Type`: Defines a set of properties and interactions with some information (i.e. the blueprint)

* `Data Structure`: Actual implementation of the concept, with all of the properties (i.e. the building itself)

---


## What data structure could we use to implement these ADTs?

* List
* Dictionary


---

## Stack (ADT) -- Sequential, LIFO

Overview: Sequential collection of objects. All operations take place at one end (LIFO).

---


### Stack (Example API) 

**Properties**:

* `push(el)`:  Add element to top of stack
* `pop`: Remove and return element from top of stack
* `peek`:  Return top element of the stack, without removing it
* `size`: Return the current size of the stack
* `empty?`: Return true or false depending on whether or not stack is empty

---

## Code Demo - Stack
```ruby
class Stack # ADT
  def initialize
    @store = [] # data structure
  end

  def push(value)
    store.push(value)
  end

  def pop
    store.pop
  end

  def peek
    store.last
  end

  def show
    store.to_s
  end

  def size
    store.length
  end

  def empty?
    store.empty?
  end

  private
  attr_reader :store
end

stack = Stack.new
stack.push(5)
stack.push(3)
p stack
p stack.pop
# p stack.store
p stack.show
```

---

## Queue (ADT) -- Sequential, FIFO

Overview: Sequential collection of objects. Removal at one end, insertion at the other (FIFO).

---

### Queue (Example API) 

**Properties:**

* `enqueue(el)`:  Add element to back of queue
* `dequeue`: Remove and return element from front of queue
* `show`:  Show the entire queue (but don't return it! Why wouldn't we want to return it?)
* `size`: Return the current size of the queue
* `empty?`: Return true or false depending on whether or not queue is empty

---

## Code Demo - Queue

```ruby
class MyQueue
  def initialize
    # instead of using an array, we can use two stacks
    @store = []
  end

  def enq(val)
    store.push(val)
  end

  def deq
    # not ideal b/c results in complete reindexing
    store.shift
  end

  def size
    store.length
  end

  def empty?
    store.empty?
  end

  def show
    store.dup
  end

  private
  attr_reader :store
end
```

---

## What makes up a Tree ADT

* Composed of nodes that store information
* Each node has (optionally) one parent and (optionally) many children
* Depth

---

## Node

+ The basic unit comprising a tree
+ Typically holds a value and references to its children
+ The root node _is_ the tree (and every other node is a sub-tree).
+ **internal nodes** vs. **leaf nodes**

---
## Node demo
```ruby
class Node
  attr_reader :value, :children

  def initialize(value, children=[])
    @value = value
    @children = children
    @parent = nil
  end

  def parent=(new_parent)
    # if self currently has a parent
      # remove self from parent children
    
    # reassign parent to new_parent

    # add self to new_parent.children (only if !new_parent.nil?)
  end
end








d = Node.new('d')
e = Node.new('e')
f = Node.new('f')
g = Node.new('g')
b = Node.new('b')
c = Node.new('c')
a = Node.new('a')

a.children << b << c
b.children << d << e
c.children << f << g
```
---
## Trees
- Which nodes are leaves?
- Which nodes are internal?

![binary-tree](https://media.geeksforgeeks.org/wp-content/cdn-uploads/binary-tree-to-DLL.png)

---

`Algorithm`: General approach and process to problem solving operations (ex. Binary Search)

`Function/Method`: Concrete implementation, in a specific language, of an algorithm (Binary Search in Ruby)

---

## Tree Traversal Algorithms (Search)

* Breadth-first Search (BFS)
* Depth-first Search (DFS)
