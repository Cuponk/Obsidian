OOP - Object Oriented Programing

Four principals of OOP
- [[#Abstraction]]
- [[#Encapsulation]]
- [[#Inheritance]]
- [[#Polymorphism]]

### #Abstraction
- The act of taking a larger, interconnected system and breaking it down into smaller components
- "An abstraction denotes the essential characteristics of an object that distinguish it from all other kinds of object and thus provide crisply defined conceptual boundaries, relative to the perspective viewer."

### #Encapsulation
- Hiding and restricting access to the internal representation of an object and only allowing users to interact with the object through public methods
- All the data and logic for an object to work should be encapsulated in the object
- Bundle data the methods that operate on that data
- Restricts access and reduces the possibility of users affecting your object in an unintended way, as you have defined the valid interactions 

### Interface vs Implementation
- Two sides of the same coin
- Encapsulation is the from the objects perspective and is concerned with the internal implementation of an object and what it exposes to the users
- Abstraction is from the perspective of other objects and is 
---
### Demo - Clock
```ruby
class Clock
     attr_accessor :sec, :min, :hrs
     def initialize
         @sec = 0
         @min = 0
         @hrs = 0
     end

     def run
         while true 
             sleep(1)
             tick
             print
         end
     end
    
     private

     def print
         puts "#{self.hrs}:#{self.min}:#{self.sec}"
     end

     def tick
         self.sec += 1
         # seconds = 1
         increment_min
         increment_hrs
     end

    
     def increment_min
         if self.sec == 60
             self.min += 1
             self.sec = 0 
         end
     end

     def increment_hrs
         if self.min == 60
             self.hrs += 1
             self.min = 0 
         end
     end

 end


clock = Clock.new.run

class Test

    def initialize
        @name = "test"
    end

    def method(name)
        rename(name)
    end
    
    private
    
    def rename(new_name)
        self.name = new_name
    end
    attr_accessor :name

end

a = Test.new
a.method("sarah")
p a
```

---
### Public, Private and Protected
- Expose limited interface
- Indicate to others how to use your code
- Can more easily refactor without changing the interface -- If a method is private, you know that now one else if relying on it so you can change it as you please

### Calling methods explicitly vs implicitly
- Implicitly is without a receiver
- Explicitly is with a receiver (like self or another instance of a class)

```ruby
    class Test
        def example_method
            self.some_method # called explicitly on `self`
            some_method # called with implicit `self`
        end
        def some_method
        end
    end
```

### #Public
- API endpoints for user - _interface_
- This is the default if no other keyword is specified
- Can be called anywhere inside or outside the class definition
- Can be called explicitly or implicitly

### #Private
- Can only be called within the class definition
- Used to be called only implicitly (except setters)
- Now can be called implicitly or explicitly
- Always will be called on self
- Helper methods should usually be private

### #Protected
- Middle ground between #Public & #Private 
- Can only be called within the class definition
- Can be called implicitly or explicitly
- Can be used on other instances of the class

### #Inheritance 

```ruby
class SubClass < SuperClass
end
```
- DRY up code by creating subtypes of existing classes
- 'Child classes' (subclasses) will have access to methods defined on their 'Parent class' (superclass)
- Subclass can only have **ONE** superclass, but superclass can have multiple subclasses

### Demo - Where will we error?
---
**Public**
```ruby
class Test
    def test_method(other_instance)
        public_method                   # a
        self.public_method              # b
        other_instance.public_method    # c
    end

    def public_method
        puts "This is a public method"
    end
end

a = Test.new
b = Test.new
a.test_method(b)
a.public_method # d
```
There is **no** error

**Private**
```ruby
class Test
    def test_method(other_instance)
        private_method                  # a
        self.private_method             # b
        other_instance.private_method   # c - error
    end

    private
    def private_method
        puts "This is a private method"
    end
end

a = Test.new
b = Test.new
a.test_method(b)
a.private_method                        # d - error
```

**Protected**
```ruby
class Test
    def test_method(other_instance)
        protected_method                  # a
        self.protected_method             # b
        other_instance.protected_method   # c
    end

    protected
    def protected_method
        puts "This is a protected method"
    end
end

a = Test.new
b = Test.new
a.test_method(b)
a.protected_method                        # d - error
```

### Demo - oop.rb
```ruby
class Dog
  def initialize(name)
    @name = name
  end

  def introduce
    puts "#{name} bork bork"
  end

  def fetch(item)
    puts "*#{name} excitedly fetches #{item} and wants you to throw it again*"
  end

  def eat(food)
    puts "*#{self.name} eats the #{food}*"
  end

  def sniff(other_dog)
    puts "*#{name} sniffs #{other_dog.name}'s butt. interesting.*"
  end
  
  protected
    attr_reader :name
	
end

```

- DRY up code by creating subtypes of existing classes
- 'Child classes' (subclasses) will have access to methods defined on their 'Parent class' (superclass)
- Subclass can only have *ONE* superclass, but superclass can have *MULTIPLE* subclasses
 

### Inheritance demo
*cat.rb*
```ruby
 require_relative 'animal'

 class Cat < Animal

   def introduce
     puts "#{name} meow"
   end

   private
   attr_reader :name
 end
```

*dog.rb*
```ruby

require_relative 'animal'

class Dog < Animal

  def introduce
    puts "#{name} bork bork"
  end

  def fetch(item)
    puts "*#{name} excitedly fetches #{item} and wants you to throw it again*"
  end

  def sniff(other_dog)
    puts "*#{name} sniffs #{other_dog.name}'s butt. interesting.*"
  end
  
end
```

*animal.rb*
```ruby
class Animal
  def initialize(name)
    @name = name
  end

 def introduce
	raise 'i need an introduce method'
 end
  
 def eat(food)
    puts "*#{self.name} eats the #{food}*"
  end
  
 protected
    attr_reader :name
```

### Inheritance pitfalls
- Inheritance created implicit dependencies
	- Inherited methods and are not listed in the subclass code
	- Multiple inheritance and mix-ins: potential for conflict
- Don't overwrite the interface!
	- Okay to change the implementation (stay DRY)
	- Okay to add to the interface

### #super

The super keyword "invokes" the parent class of the same function name
```ruby
class SuperClass
    def some_method
        puts "in SuperClass#some_method"
    end
end

class SubClass < SuperClass
    def some_method
        super # Invokes some_method in SuperClass
        puts "in SubClass#some_method"
    end
end
s = Subclass.new
s.some_method # Will print "in SuperClass#some_method" then "in SubClass#some_method"
```

### #Inheritance cont.
- Methods on subclass override those of the parent. you can invoke the parent's overridden definition of a method using `super`.
- `super` method tells Ruby to call the inherited method by the same name as the current method
- Often used in initialize if we want some shared initialization behavior for our subclass
- `super` with no parantheses passes **all arguments** to the method
- `super(arg)` with specific arguments passes **Just those arguments** to the superclass' method
- `super()` with empty parantheses passes **no arguments** to the superclass'

#### Modified cat.rb
```ruby
 require_relative 'animal'

 class Cat < Animal
   def initialize(name, fur_color)
	 super(name) #invokes init from animal.rb
	 @fur_color = fur_color
   end

   def introduce
     puts "#{name} meow"
   end

   private
   attr_reader :name
 end
```


### #Modules
- Sometimes we have shared functionality that doesn't make sense to group under a shared parent
- A module is like a class that can't be initialized - we can never have an instance of a module
- While a class can only inherit from one superclass, it can include any number of modules
- Modules don't necessitate any relationship between the classes that use them
- Modules keep out code DRY

### Demo - Modules
*walkable.rb*
```ruby
module Walkable

	def walk
	  puts "#{name} walks"
	end
```

*robot.rb*
```ruby
require_realative 'walkable'

class Robot
	include Walkable
	attr_reader :name
	
	def initialize(name)
	  @name = name
	end
	
end
```
*able to call Robot.walk from robot.rb*


### #Polymorphism
- Subclasses can override the behavior of superclass
- Each inheriting class can do something different when calling a method by the same name
- We can treat an object as the generic version, and have specific behavior determined by the particular subclass of the instance