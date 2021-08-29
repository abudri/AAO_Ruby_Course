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
