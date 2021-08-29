## [Becoming a Rubyist Notes](https://open.appacademy.io/learn/full-stack-online/software-engineering-foundations/becoming-a-rubyist-notes)

### **Use single line conditionals when possible**

When we have a single line in the body of a simple if statement (that is not attached to an elsif or else), we can turn it into a one-liner:

```
raining = true

# Less preferred
if raining
    puts "don't forget an umbrella!"
end

# Preferred by a Rubyist
puts "don't forget an umbrella!" if raining
```

### **Use built-in methods**

There are many methods in Ruby that can make your life easier. Use them:

```
num = 6

# Less preferred
p num % 2 == 0

# Preferred by a Rubyist
p num.even?
```

```
people = ["Joey", "Bex", "Andrew"]

# Less preferred
p people[people.length - 1]

# Preferred by a Rubyist
p people[-1]
p people.last
```

### **Use enumerables to iterate**

There are many enumerables in Ruby that have specific use cases. These tools can really make the code read like english. Often times, you can avoid using a while loop in favor of a more readable enumerable.

```
# Less preferred
def repeat_hi(num)
    i = 0
    while i < num
        puts "hi"
        i += 1
    end
end

# Preferred by a Rubyist
def repeat_hi(num)
    num.times { puts "hi" }
end
```

Given a problem, not all enumerables are equal. Some methods will immediately solve the problem at hand elegantly.

```
# Less preferred
def all_numbers_even?(nums)
    nums.each do |num|
        return false if num % 2 != 0
    end

    true
end

# Preferred by a Rubyist
def all_numbers_even?(nums)
    nums.all? { |num| num.even? }
end
```

### [Common Enumerables](https://open.appacademy.io/learn/full-stack-online/software-engineering-foundations/common-enumerables-notes) (`all?`, `any?`, `none?`, `one?`, `one`, `count`, `sum`, `max`, `min`, `flatten`)
Ruby's robust enumerable methods are what makes it a uniquely readable and expressive programming language. Classic enumerables like each, map, and select are staples but there are more enumerables that you will want to familiarize yourself with to write even cleaner code! This is meant to be an overview of a few methods you'll find useful, so you'll want to reference the Ruby Docs for the complete documentation of every method available in ruby!

`all?` - 
Return true when all elements result in true when passed into the block.
```
p [2, 4, 6].all? { |el| el.even? }  # => true
p [2, 3, 6].all? { |el| el.even? }  # => false
```
`any?` - 
Return true when all at least one element results in true when passed into the block.
```
p [3, 4, 7].any? { |el| el.even? }  # => true
p [3, 5, 7].any? { |el| el.even? }  # => false
```
`none?` - 
Return true when no elements of result in true when passed into the block.
```
p [1, 3, 5].none? { |el| el.even? } # => true
p [1, 4, 5].none? { |el| el.even? } # => false
```
`one?` - 
Return true when exactly one element results in true when passed into the block.
```
p [1, 4, 5].one? { |el| el.even? }  # => true
p [1, 4, 6].one? { |el| el.even? }  # => false
p [1, 3, 5].one? { |el| el.even? }  # => false
```
`count` - 
Return a number representing the count of elements that result in true when passed into the block.
```
p [1, 2, 3, 4, 5, 6].count { |el| el.even? }    # => 3
p [1, 3, 5].count { |el| el.even? }             # => 0
```
`sum` - 
Return the total sum of all elements
```
p [1, -3, 5].sum   # => 3
```
`max` and `min` - 
Return the maximum or minimum element
```
p [1, -3, 5].min    # => -3
p [1, -3, 5].max    # => 5
p [].max            # => nil
```
`flatten` - 
Return the 1 dimensional version of any multidimensional array
```
multi_d = [
    [["a", "b"], "c"],
    [["d"], ["e"]],
    "f"
]

p multi_d.flatten   # => ["a", "b", "c", "d", "e", "f"]
```
