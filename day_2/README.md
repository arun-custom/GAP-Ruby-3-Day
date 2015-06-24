#Ruby Continued

##Warmup
- Go through the arrays section of RubyMonk [here](https://rubymonk.com/learning/books/1-ruby-primer/chapters/1-arrays/).

##Array Methods

####.shift
- `.shift` will remove the first element of the array and return it.

```ruby
my_array = [1, 2, 3, 4]

my_array.shift # => 1
```

####.unshift
- `.unshift` will prepend objects to the front of the array, moving other elements upward.

```ruby
my_array = ["a", "b", "c"]

my_array.unshift("insert") # => ["insert", "a", "b", "c"]
```

####.take
- `.take` will return the first `n` elements of an array.

```ruby
my_array = [1, 2, 3, 4]

my_array.take(3) # => [1, 2, 3]
```

####.push
- `.push` will append an object to the end of an array.

```ruby
my_array = [1, 2, 3, 4]

my_array.push(5) # => [1, 2, 3, 4, 5]
```

####.pop
- `.pop` will remove the last element of the array and return it.

```ruby
my_array = [1, 2, 3, 4]

my_array.pop # => [1, 2, 3]
```

####.sort
- `.sort` will compare items in the array and sort them using the <=> operator.

```ruby
my_array = [1, 4, 2, 3]

my_array.sort # => [1, 2, 3, 4]
```

##Array Exercise
- Open the RubyMonk [array tutorial](https://rubymonk.com/learning/books/1-ruby-primer).
- Try these problems:
	- Find the length of strings in an array
	- Find the frequency of a string in a sentence
	- Select random elements from an array
	- Find non-duplicate values in an array
	- Check if all elements in an array are Fixnum
- Bonus: Try the "sort the words in a given sentence" challenge.

##Control Flow in Ruby
- Control flow allows you to direct the flow of the application depending on conditions.
- This follows the general flow of if - else with some nuances in the syntax.
- Let's take a simple example:

```ruby
name = "Arun"

if name == "Arun"
	puts "Hello Arun!"
elsif name == "Bob"
	puts "Hello Bob!"
end
```

##In-Class Lab
- Complete [rubymonk control structures subchapter](https://rubymonk.com/learning/books/1-ruby-primer/chapters/8-control-structures/).
- Complete [rubymonk objects and methods subchapter](https://rubymonk.com/learning/books/1-ruby-primer/chapters/6-objects/).

##Loops in Ruby
- There are a wide variety of loops in Ruby that make it versatile.
- There are a few different use cases for these loops, but mostly it just gives you flexibility.
- Let's look at a few examples.

#####Regular for loop
- For loops work with ranges.
- As a reminder, the two dots (..) mean inclusive of the last number, and the three dots (...) mean exclusive.

```ruby
for i in 0..5
	puts "Value of local variable is #{i}"
end
```

#####While loop
- While loops execute while a certain condition remains true.

```ruby
x = 100

while x > 0            
	x -= 1
	puts "This loop will run #{x} more times"
end
```

#####Until loop with global variables
- Until loops are similar to while loops with slightly different syntax.

```ruby
$i = 0
$num = 5

until $i > $num  do
	puts "Inside the loop i = #$i"
	$i += 1
end
```

#####Until with begin

```ruby
$i = 0
$num = 5

begin
	puts("Inside the loop i = #$i" )
	$i +=1;
end until $i > $num
```

#####Operation count
- These methods are usually reserved for if you need to perform an operation an exact number of times.

```ruby
10.times do |i|
	puts "Number is at #{i}"
end
```

#####Upto
- Upto is similar to times but is less popular.

```ruby
1.upto(3) do |i| 
	puts i * 2
end
```

##Arrays and Iterators Lab
- In this lab we will be practicing using iterators in combination with arrays to produce the results we are looking for.
- Let's start with these two arrays:

```ruby
user_names = ["Bob Jones", "Cindy Smith", "Kelsey Scott"]

user_emails = ["bob@gmail.com", "csmith@yahoo.com", "kscott@hotmail.com"]
```

- First let's start by using both loops and iterators to merge the two together.
- Your goal is to use two different approaches to merge the two arrays together so that the final structure looks like this:

```ruby
[
	["Bob Jones", "bob@gmail.com"],
	["Cindy Smith", "csmith@yahoo.com"],
	["Kelsey Scott", "kscott@hotmail.com"]
]
```

- Your goal is to replicate this effect with at least two implementations.
- After you finish this we will take it a step further and use our various iterators and loops to create a proper hash from this data.
- Your goal is to create a final structure that looks like this:

```ruby
[
	{
		name: "Bob Jones",
		email: "bob@gmail.com"
	},
	{
		name: "Cindy Smith",
		email: "csmith@yahoo.com"
	},
	{
		name: "Kelsey Scott",
		email: "kscott@hotmail.com"
	}
]
```

##Class Inheritance
- Methods can be shared from one class to another via inheritance.
- Inheritance in Ruby classes in done through the `<` operator.
- Let's take a simple example:

```ruby
class Bird  
	def preen
		puts "I am cleaning my feathers."
	end
	
	def fly
		puts "I am flying."
	end
end  
  
class Penguin < Bird
	def fly
		puts "Sorry. I'd rather swim."
	end
end  
  
animal = Penguin.new  
animal.preen  
animal.fly 
```

- In this example, the Penguin class inherits from Bird.
- Any method that is defined in the Bird class is now available in any **instance** of Penguin.

##Ruby Attributes
- You can think of attributes as instance variables that are set and read from methods within classes.
- Setting and retrieving instance variables within classes is simple, although a bit verbose.
- Ruby gives us three specific helpers to work with these variables in an easy way - attr_reader, attr_writer, attr_accessor.
- Let's have a look at each:

Let's say you have the class Person:

```ruby
class Person
end

person = Person.new
person.name # => no method error
```

We never defined a method called "name" so it doesn't work. Let's fix that:

```ruby
class Person
	def name
		@name # simply returning an instance variable @name
	end
end

person = Person.new
person.name # => nil
person.name = "Dennis" # => no method error
```

We can now read the name, but that doesn't mean we can assign the name; those are two different methods. Former called reader and latter called writer. We didn't create the writer yet so let's do that:

```ruby
class Person
	def name
		@name
	end

	def name=(str)
		@name = str
	end
end

person = Person.new
person.name = "Dennis"
person.name # => "Dennis"
```

Now we can write and read instance variable @name using reader and writer methods. Except, this is done so frequently, why waste time writing these methods every time? We can do it easier:

```ruby
class Person
	attr_reader :name
	attr_writer :name
end
```

Even this can get repetitive. When you want both reader and writer just use accessor!

```ruby
class Person
	attr_accessor :name
end

person = Person.new
person.name = "Dennis"
person.name # => "Dennis"
```

Works the same way! And guess what: the instance variable @name in our person object will be set just like when we did it manually, so you can use it in other methods.

```ruby
class Person
	attr_accessor :name

	def greeting
		"Hello #{@name}"
	end
end

person = Person.new
person.name = "Dennis"
person.greeting # => "Hello Dennis"
```

- So you may now be wondering why we would ever use attr_reader or attr_writer instead of attr_accessor every time?
- The key is signaling the intent of the program. Oftentimes you simply need to be able to read from a variable or write to it without doing both. This gives any future developer insight into how the program should function.

##Putting it Together with Super
- Super allows us to get arguments from parent methods that are of the same name.
- In the example below we have two `initialize` methods, but the sub-class is missing @wheels and @gears.
- Notice though that using `super` in the sub-class allows us to grab @wheels and @gears from the `initialize` method of its parent class.

```ruby
class Bicycle  
    attr_reader :gears, :wheels, :seats  
    
    def initialize(gears = 1)  
        @wheels = 2  
        @seats = 1  
        @gears = gears  
    end  
end  

class Tandem < Bicycle  
    def initialize(gears)  
        super  
        @seats = 2  
    end  
end

t = Tandem.new(2)  
puts "Gears: " + t.gears.to_s
puts "Wheels: " + t.wheels.to_s
puts "Seats: " + t.seats.to_s

b = Bicycle.new  
puts "Gears: " + b.gears.to_s
puts "Wheels: " + b.wheels.to_s  
puts "Seats: " + b.seats.to_s
```

##Inheritance Lab
- Now that you've seen how inheritance works, let's test it out in the wild.
- We will practice a series of array exercises while using methods that pull from classes within modules.
- Here are the steps you will need to follow:
	- Step 1: Create a module called "Helpers" and a class inside that module called "ArrayHelpers".
	- Step 2: Use this class to create generic methods that will perform operations to accomplish the below problems.
	- Step 3: Create a class outside of this module that inherits from your ArrayHelpers class that will call upon your helper methods to address the below problems.

#####1. Find the last name in the following array:

```ruby
[
    'Moe', 
    'Larry', 
    'Curly',
    'Jane',
    'Emma',
    'Elizabeth',
    'Elinor',
    'Mary',
    'Darcy',
    'Grey',
    'Lydia',
    'Harriet'
]
```

#####2. Add your name to the end of the friends and add another name to beginning. Change the Elizabeth to Liz.

#####3. Sort the list of friends above.

#####4. Given a list of ages, find the median age:

```ruby
[83, 53, 37, 29, 60, 30, 66, 19, 59, 41, 9, 64, 19, 80, 24, 53, 70, 1, 53, 40, 92, 4, 71, 65, 8, 2, 51, 80, 94, 37, 80, 64, 19, 6, 14, 32]
```

#####5. There are a list of names in a string, below. How could we sort them? Hint: use string and array methods.

```ruby
"Moe,Larry,Curly,Jane,Emma,Elizabeth,Elinor,Mary,Darcy,Grey,Lydia,Harriet"
```

#####6. List all the friends above in reverse alphabetical order.

#####7. Combine the two lists below and sort them:

```ruby
my_friends = [
      'Rickon',
      'Meera',
      'Hodor',
      'Jojen',
      'Osha',
      'Rickard',
      'Maester',
      'Rodrik',
      'Jory',
      'Septa',
      'Jon'
]

your_friends = [
      'Bilbo',
      'Boromir',
      'Elrond',
      'Faramir',
      'Frodo',
      'Gandalf',
      'Legolas',
      'Pippin'
]
```