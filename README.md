# Ruby Cheat Sheet

_Note:_ Format later, look into `md` formating. Using *The Ruby Way* to learn Ruby (will 
not cover it all though; certain chapters are not useful to me)

## Purpose

At work I've been just googling everything but should really remember certain things.
People praise Ruby as being fun to code in, Rails sucks but Ruby can be fun so time to 
properly learn it - even though it is dreadfully slow. :(

## Questions to answer

List of questions that I have while learning. I can come back to write them here.

- Is Ruby a purely OOP language? Yes

## Overview/random notes on Ruby

- An `Object` contains the following:
  - attributes
  - methods
- Garbage collection (GC) handles destructors
- Ruby does not allow multi-inheritence
- Abstract classes can be written but in a hack-ish way
- When writing in Ruby, the goal should **ALWAYS** be to make it readable. (example would be
using `unless` instead of `if !`)
- Comments are obvious _EXCEPT_ that multiline comments use `=begin` and `=end`
- `===` is defined by the class. It is ambigious.


--
Side note about blocks, procs, and lambdas:
- Proc and Lambda are essentially just blocks so that you can define once and just reference it
- Converting a Proc to a block uses the `&` operator
- Difference between lambdas and procs are that returns are different and lambdas check number of arguments

Example:

```
proc = Proc.new { |x| x * 2 }
[1,2,3].each(&proc)
```

- `.dig` is also very useful, use it inplace of `&.`
- `&:` calls method on variable

Example:

```
[1,2,3].each(&:to_s)
```
## Keywords and naming conventions

Certain keywords can't be overwritten. They are ones that you won't overwrite anyways
so no need to watch out for these.

Naming conventions are important:
(from the book)
- `local_variables` lowercase letter or an underscore.
- `$global_variables` begin with $ **(NEVER USE BUT KNOW)**
- `@instance_variables` (within an object) begin with @
- `@@class_variables` (within a class) begin with @@
- `CONSTANTS` are in all capital letters

## Strings

Single vs Double quote:
- Use single most of the time unless interpolation is required. Single is much more strict
only few escape characters.

Can append to string using `<<`
Can convert a string to a int/float using `to\_i` or `to\_f`
Initialize `Float` and `Integer` using the following: `Integer('number')` since this returns an errors.

Interpolation formula: (Double quotes) "#{var} something something"

**NOTE:** Strings are very similar to arrays and vice versa. They share many methods.

Useful methods:

- `length/size` - get char count
- `insert` - insert string in position `string.insert(3, 'test')`
- `split` - return an array of tokenz `string.split(' ')`
- `%w[some kind of string]` = returns tokenized array
- `sub / gsub / delete` - alter the string
- `include?` - contains a string
- `index` and `rindex` (rindex just starts at the right side)
- `downcase / upcase / capitalize`
- `puts` vs `print` is that `puts` adds new lines.
- `to\_s` vs `to\_str`, former is defined by class to not return garbage
- `join` to join tockenized string array

## Skipping the Regex section for now, can go back to it later

## Internationalization in Ruby

- Ruby uses UTF-8 as the default (which is pretty much just ASCII)
- `i18n` is a gem we use where we have a config file that is used for translation purposes
- By setting the local language, get the YAML which determines what to write
- located in `local/[language].yml`

That is pretty much it for this chapter. Just understanding how encoding works - which I don't
feel I need to learn in depth and using the `i18n` gem for different languages.

## Performing Numerical Calculations

_Overview: Very extensive topic but not required when building CRUD apps - at least not the one I am currently working on so most of this goes to the wayside._

Binary: `0b10010`
Hex: `0x0034`
Octal: `01234` - **with a 0 in-front, good to note this**

For longer numbers, use `_` to denote commas, just easier to read even though it doesnt do anything.

`Float::MIN` && `Float::MAX` are defined

`**` used to exponent

Useful methods:

- `floor`
- `ceil`
- `round`
- `to_f` and `to_i`

## Symbols and Ranges

_Overview: Symbols are mainly just immutable strings, a lot of times you can replace one for the
other. Know_`to_s`_ and _`to_sym`_. For Range, know that to to initialize, use parenthesis and
about_ `to_a`.

- `..` vs `...`: Former is inclusive of upper bound, latter is not.

- Symbols are immutable strings; being immutable means that they share the same memory address.
Example: [:sym, :sym] will use the same memory address.
- Symbols can be defined from strings like `:"hello world"`, might be a little weird though
- Use Symbols if you never need to change their values: ex direction[:north, :east, :south, :west]
- String to Symbol and vice versa = `to_s` and `to_sym`

- `..` inclusive, `...` exclusive

Useful methods:
- `first` and `last`
- `to_a`
- `include?`
- Range is defined using parenthesis

## Working with Time and Date

_Overview: two objects of Date and Time, these rarely come up so for the most part just google
it, mainly just going to be using Time.now._

Centered around `Time` and `Date` object.

Time is more about the current, Time == 12 am
Date is about a set day

Useful methods:
- `new`
- `now`
- `[y/w]day
- `utc` for the standard time
- `zone`
- `local` to equate to local time zone
- `.hour`
- `.min`

epoch! Seconds that have elapsed since January 1, 1970. To get this, simple just `to_i`

## Arrays, Hashes, and Other Enumerables

Arrays:

Monster, there are so many things you can do with arrays. It is pretty crazy. 

*Note to self*: compile a list of methods and things from top down of what is most important.

Useful methods:
- `values_at` (can take a range, returns an array)
- can determine where to start and the end point - similar to Strings
- `length` and `size` (size is an alias)
- `sort` - built in sorting method
- `detect` or `find` (alias) to find the first
- `find_all`/`select` to return an array that matches
- `reject` is the complementary method to `select`
- `min` and `max`
- `.index` an array to get the index instead
- `sample` to get a random value
- `delete` and `delete_at` for index
- `delete_if` deletes if block is true
- `compact` removes all `nil` values
- `slice` removes element from array
- `shift` and `pop` to remove the front and back of an array
- that is for removing, to add to from or back, just concatentate
- can add `with_index` after `each`
- `uniq` is also useless

Initializing an array is pretty obvious EXCEPT that you can state the size and default value:
`Array.new(10, "anything")` or `Array.new(3)`

- arrays can accept a Ranges (arr[0..3])
- you can even replace an array using a range (arr[2..4] = [123,123,123])
- NOTE: arr[2..2] = [123,123,123] would insert it there

Hashes:

Initialize, can be through `new` or just create a hash and assign it.
Example: var = {one: "something", two: "something else"}

Useful methods:
- `to_a` and `to_h`
- `to_h` from an array requires an array within an array with 2 elements [[something, else]]
- `fetch` will return an exception if the hash is not found - much more useful I would say
- interating with `|key, value|`
- `delete` using key
- can use other methods too such as `delete_if`, `shift`, couple others
- use `key?` or `include` to determine if hash is there
- `keys` and `values` to get an array of their respective outputs
- `merge` to merge two hashes, can include block

Enumerations:

Useful methods:

- `any?` and `all?` check if `nil` or accept a block
- `each.with_index |x,i|`
- `find_index(val)`
- `first / last + (val)` example `first` or `first(5)`
- `one?` then block
- `none?` then block
- `count` or `count(val)` or `count + block`



## More Advance data structures

This could be nice

= Turned out to be pretty useless, it just covers a small subset of data structures such as
stacks, queues, binary trees, graphs, but there are better resources to learn that stuff.
I am only interested in learning about Ruby coding.

## OOP and Dynamic Features in Ruby

HUGE!!

Class should have `initialize` method which is called with `new` is issued.

`attr_accessor` :symbol gives getters and setters
`attr_reader` :symbol gives getters
`attr_writer` :symbol gives setters | this can be within the `protected` section

When changing the values above, this requires `self.attribute` OR `@attribute`.

Access to global variables within a class use `::`

`is_a?` or `instance_of` to determine if it is that type of Class

`private` = only the class itself can reference this
`protected` = class and subclasses

`freeze` method makes it so you can't alter it afterwards - probably for saftey reasons

Kinda just skimmed this over since it is getting late - will revise.

## There are other sections that I could read when I have time but as of now, it shouldn't
be my main concern.
