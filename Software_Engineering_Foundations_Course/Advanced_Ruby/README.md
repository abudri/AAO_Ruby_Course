## [Becoming a Rubyist Notes](https://open.appacademy.io/learn/full-stack-online/software-engineering-foundations/becoming-a-rubyist-notes)

### **Use single line conditionals when possible**

When we have a single line in the body of a simple if statement (that is not attached to an elsif or else), we can turn it into a one-liner:

```ruby
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

```ruby
num = 6

# Less preferred
p num % 2 == 0

# Preferred by a Rubyist
p num.even?
```

```ruby
people = ["Joey", "Bex", "Andrew"]

# Less preferred
p people[people.length - 1]

# Preferred by a Rubyist
p people[-1]
p people.last
```

### **Use enumerables to iterate**

There are many enumerables in Ruby that have specific use cases. These tools can really make the code read like english. Often times, you can avoid using a while loop in favor of a more readable enumerable.

```ruby
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

```ruby
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
```ruby
p [2, 4, 6].all? { |el| el.even? }  # => true
p [2, 3, 6].all? { |el| el.even? }  # => false
```
`any?` - 
Return true when all at least one element results in true when passed into the block.
```ruby
p [3, 4, 7].any? { |el| el.even? }  # => true
p [3, 5, 7].any? { |el| el.even? }  # => false
```
`none?` - 
Return true when no elements of result in true when passed into the block.
```ruby
p [1, 3, 5].none? { |el| el.even? } # => true
p [1, 4, 5].none? { |el| el.even? } # => false
```
`one?` - 
Return true when exactly one element results in true when passed into the block.
```ruby
p [1, 4, 5].one? { |el| el.even? }  # => true
p [1, 4, 6].one? { |el| el.even? }  # => false
p [1, 3, 5].one? { |el| el.even? }  # => false
```
`count` - 
Return a number representing the count of elements that result in true when passed into the block.
```ruby
p [1, 2, 3, 4, 5, 6].count { |el| el.even? }    # => 3
p [1, 3, 5].count { |el| el.even? }             # => 0
```
`sum` - 
Return the total sum of all elements
```ruby
p [1, -3, 5].sum   # => 3
```
`max` and `min` - 
Return the maximum or minimum element
```ruby
p [1, -3, 5].min    # => -3
p [1, -3, 5].max    # => 5
p [].max            # => nil
```
`flatten` - 
Return the 1 dimensional version of any multidimensional array
```ruby
multi_d = [
    [["a", "b"], "c"],
    [["d"], ["e"]],
    "f"
]

p multi_d.flatten   # => ["a", "b", "c", "d", "e", "f"]
```

### [Symbols Notes](https://open.appacademy.io/learn/full-stack-online/software-engineering-foundations/symbols-notes)

#### My Main Takeaways
* **TLDR**: symbols are more memory efficient, operators are thus faster, they are immutable so good for hashes and unique keys
* Both strings and symbols contain many characters, but they are not equivalent. The most apparent difference between strings and symbols is that strings are mutable, while **symbols are immutable**. This means that string can be "changed", but a symbol can never be "changed". The utility of a symbol comes from the fact that it can never change over time. The technical implication of this is that a symbol only needs to be "created" once. There is no need to create "copies" of symbol because we can be certain that it will not change over the course of our programs. Operations such as comparing two symbols is **very fast and efficient** compared to regular strings.
* Under the hood, each time we reference a literal string, Ruby will allocate a piece of our machine's memory to store that string. More memory must always be allocated for a new string, even if it is a duplicate value, because strings are mutable! We must track changes to the strings separately, so we need to store the two instances of the string in distinct memory locations.
* Because of these characteristics, symbols are often used to act as unique identifiers in our code. We'll be able to ensure the the identifier will remain intact, without change, while also **being efficient with memory**.

#### **Symbols**

Ruby has an additional data type that is similar to Strings, called **Symbols**. Let's explore what differentiates a Symbol from a String, and how to use them in our code. In Ruby, we can denote a symbol using a colon (:) before writing characters. Where a string is wrapped in quotes, a symbol just has a leading colon. Both strings and symbols contain many characters, but they are not equivalent.

```ruby
str = "hello"   # the string
sym = :hello    # the symbol

p str.length    # => 5
p sym.length    # => 5

p str[1]        # => "e"
p sym[1]        # => "e"

p str == sym    # => false
# a string is different from a symbol!
```

# **Symbols are Immutable**

The most apparent difference between strings and symbols is that strings are mutable, while **symbols are immutable**. This means that string can be "changed", but a symbol can never be "changed":

```ruby
str = "hello"
sym = :hello

str[0] = "x"
sym[0] = "x"

p str   # => "xello"
p sym   # => :hello
```

The utility of a symbol comes from the fact that it can never change over time. The technical implication of this is that a symbol only needs to be "created" once. There is no need to create "copies" of symbol because we can be certain that it will not change over the course of our programs. Operations such as comparing two symbols is very fast and efficient compared to regular strings.

**Under the hood**, each time we reference a literal string, Ruby will allocate a piece of our machine's memory to store that string. More memory must always be allocated for a new string, even if it is a duplicate value, because strings are mutable! We must track changes to the strings separately, so we need to store the two instances of the string in distinct memory locations.

Talk of memory locations is pretty abstract, but an easy way to witness this is to use Ruby's `object_id` method. This will return the memory address of some data. Notice how duplicate value strings will be stored at different memory locations:

```ruby
"hello".object_id   # => 70233443667980
"hello".object_id   # => 70233443606440
"hello".object_id   # => 70233443438700
```

If we don't intend to mutate the string, we can use a symbol to save some memory. A symbol value will be stored in exactly one memory location:

```ruby
:hello.object_id    # => 2899228
:hello.object_id    # => 2899228
:hello.object_id    # => 2899228
```

Because of these characteristics, symbols are often used to act as unique identifiers in our code. We'll be able to ensure the the identifier will remain intact, without change, while also being efficient with memory.

# **Symbols as hash keys**

We'll see the preference of using of symbols in a few places in Ruby. For now, one common way to a symbol is as the key in a hash:

```ruby
my_bootcamp = { :name=>"App Academy", :color=>"red", :locations=>["NY", "SF", "ONLINE"] }
p my_bootcamp           # => {:name=>"App Academy", :color=>"red", :locations=>["NY", "SF", "ONLINE"]}
p my_bootcamp[:color]   #=> "red
```

When initializing a hash with symbol keys, Ruby offers a shortcut. We can drop the rocket (=>) and move the colon (:) to the right of the symbol:

```ruby
my_bootcamp = { name:"App Academy", color:"red", locations:["NY", "SF", "ONLINE"] }
p my_bootcamp           # => {:name=>"App Academy", :color=>"red", :locations=>["NY", "SF", "ONLINE"]}
p my_bootcamp[:color]   #=> "red
```

This shortcut is **only allowed when initializing the symbols in the hash**. When getting a value from the hash after initialization, we must always put the colon on the left like normal. `hash[:key]` is the correct syntax. Writing `hash[key:]` is invalid.


### [Symbols Lecture (Video)](https://open.appacademy.io/learn/full-stack-online/software-engineering-foundations/symbols-lecture)

A lot of string methods like index `.[]` or `.length` are also available for symbols:

```irb
irb(main):012:0> :hello[1]
=> "e"
irb(main):013:0> :hello.length
=> 5
```

Strings are also **mutable**, but **symbols are immutable**, for a simple example see how we can change the string below, but we can not change a symbol:

```irb
irb(main):014:0> str = "hello"
=> "hello"
irb(main):015:0> str[1] = "x"
=> "x"
irb(main):016:0> str
=> "hxllo"
irb(main):017:0> sym = :hello
=> :hello
irb(main):018:0> sym[1] = "x"
Traceback (most recent call last):
	19: from /Users/z/.rbenv/versions/2.6.3/bin/irb:23:in `<main>'
	18: from /Users/z/.rbenv/versions/2.6.3/bin/irb:23:in `load'
	17: from /Users/z/.rbenv/versions/2.6.3/lib/ruby/gems/2.6.0/gems/irb-1.3.5/exe/irb:11:in `<top (required)>'
(irb):18:in `<main>': undefined method `[]=' for :hello:Symbol (NoMethodError)
irb(main):019:0> sym[1] = x
Traceback (most recent call last):
	19: from /Users/z/.rbenv/versions/2.6.3/bin/irb:23:in `<main>'
	18: from /Users/z/.rbenv/versions/2.6.3/bin/irb:23:in `load'
	17: from /Users/z/.rbenv/versions/2.6.3/lib/ruby/gems/2.6.0/gems/irb-1.3.5/exe/irb:11:in `<top (required)>'
(irb):19:in `<main>': undefined local variable or method `x' for main:Object (NameError)
```

Also, the same string value like `"hello"` can and is stored many times in memory, since it can change and mutate, but a symbol will always only have one memory address.  Can't change them so easy to store that info in your computer.

Symbols are about under the hood things, but to put it shortly, most important thing is symbols are overall going to be more efficient than strings in our computer and are good for quick lookup, and a hash is exactly that scenario.

### [Option Hashes](https://open.appacademy.io/learn/full-stack-online/software-engineering-foundations/default-arguments-and-option-hashes-notes)

If you have a method that accepts a hash as an argument, you can omit the braces when passing in the hash:

```ruby
def method(hash)
    p hash  # {"location"=>"SF", "color"=>"red", "size"=>100}
end

method({"location"=>"SF", "color"=>"red", "size"=>100})

# this also works:
method("location"=>"SF", "color"=>"red", "size"=>100)
```

This can really clean things up when you have other arguments before the hash:

```ruby
def modify_string(str, options)
    str.upcase! if options["upper"]
    p str * options["repeats"]
end

# less readable
modify_string("bye", {"upper"=>true, "repeats"=>3}) # => "BYEBYEBYE"

# more readable
modify_string("bye", "upper"=>true, "repeats"=>3)   # => "BYEBYEBYE"
```

Combining this with the default arguments we covered in the previous section can make our code even more flexible:

```ruby
def modify_string(str, options={"upper"=>false, "repeats"=>1})
    str.upcase! if options["upper"]
    p str * options["repeats"]
end

modify_string("bye")   # => "bye"
modify_string("bye", "upper"=>true, "repeats"=>3)   # => "BYEBYEBYE"
```

[Default Arguments](https://open.appacademy.io/learn/full-stack-online/software-engineering-foundations/default-args-and-option-hashes-lecture)

```ruby
def repeat(str, n)
  p str * n
end

repeat("hi", 3)  # "hihihi"
repeat("hi") # Error: should error for missing 2nd argument
```

we can change the above to give default behavior of printing out `"hi"` just once,

```ruby
def repeat(str, n=1)
  p str * n
end

repeat("hi", 3)  # "hihihi"
repeat("hi") # "hi"
```

You can do the same with hashes, say you want a method that prints out a hash

```ruby
def print_h(hsh)
  p hsh
end

print_h( { "city"=>"ny", "color"=>"red" } )
```

When you pass in a hash as an argument to a method, you can actually remove the curly braces `{ .. }`, since Ruby sees the first argument is a key-value pair, it interprets and treats the rest of the input as a hash, so you can do:

```ruby
print_h( "city"=>"ny", "color"=>"red" )
```

You can take this further and have a non-hash argument before the hash argument like a string of `name`, 

```ruby
def print_h(name, hsh)
  p name
  p hsh
end
```

You can do,

```ruby
print_h( { "Abdullah", "city"=>"ny", "color"=>"red" } )
```
Ruby will see the first argument is not a key-value pair, so it is interpreted as a string and not interpreted as part of the hash, and the next argument is a key-value pair, so that and all following arguments will be included as data inside your hash.

This is just a cleaner way of doing things.




