


```
#                eosRnuirc
#               eosR  nuirc
#              eo  sR nu  irc
#             e o s R n u i rc             
#             e o s R n u i r c
#             e o s R u n i cr
#              eo  Rs un  cri
#               Reso  curin
#                Recursion
```

Note: This shows the merge sort algorithm

---

## What is a recursive function?

* Calls itself ("recurses")
* Solves a problem by breaking it down into smaller subproblems
* Has a _**base case**_ – simplest "already solved" condition
* Builds back up incrementally using an _**inductive step**_ (more to)

---

## Inductive Step
How we use the return value of the previous step to determine the current result.

---

# Movie Theater Example
How do you know what row you are in in a dark theater?

---

## Problem Solving Process
1. Understand the problem
1. Identify Base case
1. Write one step up from base case
1. Logic for inductive step
1. Code it out!

---

## Code Demo

```ruby
def iter_sum(n)
  (0..n).inject { |acc, ele| acc + ele }
end

# p iter_sum(100)

def rec_sum(n)
  return 0 if n == 0
  rec_sum(n-1) + n
end

# p rec_sum(5)

def rec_reverse(str)
  return '' if str.length == 0
  str[-1] + rec_reverse(str[0...-1])
end

# def rec_reverse!(str)
#   return str if str.length == 0

# end

class String
  def rec_reverse
    return '' if self.length == 0
    self[-1] + self[0...-1].rec_reverse
  end
end

# p rec_reverse('hello world') # 'dlrow olleh'
# p rec_reverse('') # ''

FIB_COUNT = Hash.new(0)
def fibs(n, memo = {})
  return 1 if n < 2
  return memo[n] if memo.has_key?(n)
  FIB_COUNT[n] += 1
  memo[n] = fibs(n-2, memo) + fibs(n-1, memo)
  memo[n]
end

# p fibs(5)
p fibs(1000)
p fibs(2000)
# p FIB_COUNT
```

---

## The power of Memoization!
![fibs_memoized](https://aa-ch-lecture-assets.s3.us-west-1.amazonaws.com/ruby/recursion/memoization_alternative.png)

---

## Strategy
 1. Simplify the problem
 2. Identify the base case
 3. Write the inductive step

---

## Final Thoughts
- Assume what your last recursive call should return  
and build out your inductive step from there
- Use small examples to visualize things
	- one or 2 steps up from the base case
- Look at how you can reduce the input on each call
	- Arrays and Strings: shorten them
  - Integers: decrease or increase to a base case
- Return the same data type (base case and final)

---

## Remember
* You can use Recursion and Iteration _together_
* Each recursive call will return before anything else happens - just like any method call
* Always assume you're getting back the same data type!

---
