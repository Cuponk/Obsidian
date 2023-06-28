
## Guidelines 
* Style is essential
* During interviews, poor code style is a dead giveaway that someone lacks experience. 
* Good ruby code should **read like English**.

---

## Rules 

#### Snake, pascal case, screaming snake in Ruby
```ruby 
  variable_names = 🐍 "snake_case" 
  ClassNames = 🐫 "UpperCamelCase" aka "PascalCase" 
  CONSTANTS = 😱 🐍"SCREAMING_SNAKE_AHHHH!" 
```

---


#### Single line `if` / `unless` 
```ruby 
  if truthy_thing? 
    # multiple 
    # lines 
  end 
  puts "truthy!" if truthy_thing? # single line! 
```

---

#### 80 character limit for lines 
```ruby 
rant = "You could write really, really, really long lines in Ruby but that is bad code style should be avoided.  Do not have more than 80 characters on one line." 
```
---

#### Interpolation > Concatenation 
```ruby 
  name = "Markov" 
  puts "Why, hello there " + name + ", have a lovely day!" 
  puts "Why, hello there #{name}, have a lovely day!" 
```

---

#### Use `!` for mutating methods, `?` for boolean methods 
```ruby 
  "abc".upcase! 
  [1, 2, 3].reverse! 
  5.even? 
  "abc".is_a?(String) 
```

---

#### Prefer block parameters over `yield` 
**More explicit: 
```ruby 
  def do_the_thing(x, &prc) 
      prc.call(x) 
  end 
``` 
Less explicit: 
```ruby 
  def do_the_thing(x) 
      yield(x) 
  end 
```

---

#### Use proper spacing and indentation 

```rb 
def my_function 
  system("clear") 
  puts "Let's do this thing!" 
   
  loop do 
    arr = [] 
    until arr.length == 6 
      until letter 
        letter = gets.chomp 
        if not_valid?(letter) 
           puts "Wrong." 
           letter = nil 
        end
	  end 
      arr << letter 
    end 
  end 
  puts "The result is: #{arr}" 
end 
```

---

#### No one-letter variable names 
Exhibit A: 
```rb 
def do_something(f, s) 
  x = nil 
  until x == s 
    x = @y.z(f) 
    a(x) unless v?(x) 
    x = nil 
  end 
  puts "Congratulations!" 
end 
```

---
#### No one-letter variable names 2
Exhibit B:
```rb
def do_something(prompt, answer)
  input = nil
  until input == answer
    input = @current_player.guess(prompt)
    unless valid_guess?(input)
      alert_invalid_guess(input) 
      input = nil
    end
  end
  puts "Congratulations!"
end
```
Which one would YOU rather your teammate wrote?

---
### Caveat
* Exception to this is loops.
* But even for loops, good to use more meaningful names.
* Especially when using nested loops.
---


### Variables

+ Ruby variables hold *references* (otherwise known as *pointers*) to objects stored in memory
+ `=` assignment operator
  + _assigns_ the variable pointer
  + doesn't change or *mutate* the object stored in memory

---

### Mutability

+ Mutable: state can be modified after it is created
+ Immutable: state cannot be modified after it is created

| Mutable  | Immutable   |
|----------|-------------|
| `String` | `Integer`   |
| `Array`  | `Float`     |
| `Hash`   | `Symbol`    |

---

### Reference Diagram + Demo

---
```ruby
## Part 1

a = 7
a.object_id
a.object_id == 7.object_id

# Integers are immutable (same every time)
7.object_id
7.object_id
7.object_id
7.object_id == 7.object_id

# Strings are mutable (different every time)
"hello".object_id
"hello".object_id
"hello".object_id
"hello".object_id == "hello".object_id # false

# Reassignment
b = 9
old_a_id = a.object_id
old_b_id = b.object_id
a += b
a.object_id
a.object_id == old_a_id # false
b.object_id == old_b_id # true - we didn't change b, only a

# Take questions from class and demo them in console as long as they are 
# reasonable and in scope

## Part 2

a = [1,2,3]
a.object_id 
a[0].object_id
a[0].object_id == 1.object_id # true - array indices are references themselves

b = a
b.object_id
a.object_id == b.object_id # true

a[1] = 4
a
b
a.object_id == b.object_id # still true - we didn't reassign a, we reassigned an index of the array it references (the same array b references)

# Take questions from class at this stage and demo as necessary

old_a_id = a.object_id
a.push(2)
a
b # We will see that b was also changed by pushing onto a
old_a_id == a.object_id # true - we mutated `a`, we didn't reassign it
a.object_id == b.object_id # since we didn't reassign a, it's still referencing the sam array as b, that's why b had also changed when we looked at it

old_b_id = b.object_id
b.concat([5,6,7])
b
a # see that it was also modified - `concat` mutates its receiver
old_b_id == b.object_id # true
a.object_id == b.object_id # true

old_a_id = a.object_id
a += [8, 9]
a
b # not modified - we reassigned a, therefore b was unaffected
a.object_id == b.object_id # false, we reassigned a
old_a_id ==  a.object_id # false, same reason
```

---

# Scope

---

## Different kinds of variables
* **Local variables**
* Global Variables
* Instance variables
* Class Variables

---

### Block Scoping (of local variables)
* Inside of a `do..end` block, you have access to all variables declared previously (higher) in your code and at the same or an outer-level scope.
* Variables *declared* within a block, are not accessible to the outer scope
  * However, if a variable is declared in outer-level scope, *changes* made to variable in inner-level scope persist when back at outer-level.

---

### Scope "Gates"
Parts of Ruby code in which an *entirely* new scope is created and all local variables previously defined are no longer accessible (i.e. you do not have access to local variables defined in outer scopes). The three main scope gates are:
1. Method definitions
2. Class definitions
3. Module definitions

---

## Parameters vs Arguments

* **Parameter** - variable in a method _definition_
* **Argument** - variable method is _invoked_ with

---

## Passing arguments to methods

* In the scope of a method, the parameter is a copy of the argument that the method was invoked with - both are references
  * In essence another reference is created, that points to the same spot in memory as the argument passed in
* Therefore if we _reassign_ the parameter within the method, the argument that the method was invoked with is unaffected
* But if we _mutate_ the parameter within the method, this affects the argument the method was invoked with (since it is pointing to the same object)

---

## Making Array of Arrays

* Naive Approach: `Array.new(3, [])`
* Correct Approach(es): `Array.new(3) { [] }` || `Array.new(3) { Array.new }`

---

## Making Hash with Array default

* Naive Approach 1: `Hash.new([])`: The default could be mutated!
* Naive Approach 2: `Hash.new { [] }`: does not store keys into the hash!
* Correct Approach: `Hash.new { |h, k| h[k] = [] }`

---

## Creating a Counter Hash
* `Hash.new(0)`: works fine because we can't mutate Integers

