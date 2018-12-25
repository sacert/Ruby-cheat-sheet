# Ruby Cheat Sheet
----

_Note:_ Format later, look into `md` formating. Using *The Ruby Way* to learn Ruby (will 
not cover it all though; certain chapters are not useful to me)

## Purpose: 

At work I've been just googling everything but should really remember certain things.
People praise Ruby as being fun to code in, Rails sucks but Ruby can be fun so time to 
properly learn it - even though it is dreadfully slow. :(

#### Questions to answer:

- Is Ruby a purely OOP language? Yes


#### Overview notes on Ruby:

Object - contains attributes and methods
When class is created, becomes instantiated (instance is created: that is the object) 
Has a constructor but NOT a destructor - garbage collection handles that.
Multiple inheritence is a no-go.
No abstract classes - can be hacked together though.

When writing in Ruby, the goal should *ALWAYS* be to make it readable. (example would be
using `unless` instead of `if !`

Interpreted language. Slower because of this but faster prototyping.

#### Keywords and naming conventions:

Certain keywords that can't be overwritten. They are ones that you won't overwrite anyways
so no need to watch out for these.

Naming conventions are important:

The book has the following:

• Local variables (and pseudovariables such as self and nil) begin with a
• lowercase letter or an underscore.
• Global variables begin with $ (a dollar sign).
• Instance variables (within an object) begin with @ (an at sign).
• Class variables (within a class) begin with @@ (two at signs).
• Constants begin with capital letters.
• Special variables starting with a dollar sign (such as $1 and $/) are set by the Ruby
interpreter itself.

To shorten, use common sense. It is the same for almost every language except global variables
start with a `$`, class variables start with a `@@`, and although it states that constants begin
with a capital, make the entire variable name in all caps because that is how it is for every
other language..

#### Random bits

_Guess casue it is the overview section that these things are included, they have their own sections
so don't need to go over this too much_

Comments are obvious _EXCEPT_ that multiline comments use `=begin` and `=end` cause why not.

The difference between a single quote and double quote string is that single quote strings are as is.
Meaning you don't alter them, maybe poor wording, but with double quotes you can use interpolation. `#{var}`
Our code has a mix of double and single quotes littered everywhere. Try to be consistent when writing your own code.

Interperted language means spaces matter! Use them carefully or you will recieve a lot of errors.

!!! Ruby has no Boolean class...???

`===` is defined by the class. When to use? I guess it depends.
For Range, it looks if it is within that range. (Ex. (1..4) === 2)
For a Class, it looks if they share the same class (Ex. String === "hi")

`..` vs `...`:
Former is inclusive of upper bound, latter is not.

@@ has a class wide scope - contain some shared memory.
@ instance variable, limited to the scope of instantiation.

Ruby constants are a *LIE*, they can be changed outside the instance. Just not within them.


---------------

Okay that was just a lot of fluff just thrown around but now for some actual drilled down stuff.

## Strings:

Rough notes: More to add whenever I can. No need to memorize everything here.

Single quote:
A lot more strict - very literal. Escape character only for `'` and `\`
Double quote:
Use for interpolation and escape characters.

Useful methods:

- `length`\`size` (size is an alias)
- `each/\_[char/byte/line]
- `split ( ",", num)` = returns tokenized array
- `%w[some kind of string] = returns tokenized array
- `lowercase`, `uppercase`, `capitalize`
- `split` and `join`
- `reverse`
- `delete` to remove certain characters

You can get a substring by using an array, giving either Range or starting points & how many 
to get. Ex str[6, 2], get 2 characters after the 6th character.

- sub & gsub, sub just changes the first things while gsub looks at the entire string.
- index & rindex (rindex just starts at the right side)
- include? - string match

HUGE! `puts` vs `print` is that `puts` adds new lines.

- `to\_s` vs `to\_str`. Former should return a string of the object, likely to give me garbage. 
The latter will be defined in the class to constuct how I want to return a string.
- Can append to string using `<<`
- Can convert a string to a int/float using `to\_i` or `to\_f`
But also note that something it is better to use `Integer('123')` or `Float`. Returns
an error and can be useful for binary representations.
- Can use `count` to count the number of characters

## Skipping the Regex section for now, can go back to it later

## Internationalization in Ruby

_This section seems a bit premature to be reading but whatever. Likely not ganna write many 
on the topic for now._

- Ruby uses UTF-8 as the default (which is pretty much just ASCII)
- `i18n` is a gem we use where we have a config file that is used for translation purposes
- By setting the local language, get the YAML which determines what to write
- located in `local/[language].yml`

That is pretty much it for this chapter. Just understanding how encoding works - which I don't
feel I need to learn in depth and using the `i18n` gem for different languages.

## Performing Numerical Calculations

_Overview: Cool stuff here but not required when building CRUD apps - at least not the one I am
currently working on._

Cool, so you can express binary in the following:
`0b10010`
Hex:
`0x0034`
Octal:
`01234` - with a 0 infront (Might have to be careful of that)

For longer numbers, use `_` to denote commas, just easier to read even though it doesnt do anything.

Somethings to note are that Float has constants for MIN and MAX.

`**` used to exponent

Useful methods:
- `floor`
- `ceil`
- `round`

- For large/small numbers, use `BigDecimal` and `Bignum` - this is cool but unlikely to use
very large numbers within Ruby.

- Rationals, use `Rational` - again very unlikely to be using this

There are ton of other mathematical operations such a matrix/vector multiplication, handling
bytes, trig functions, logs, etc. Bottom ground, there are a TON of stuff, and some really cool
stuff like built in variance/standard deviation calculations but I'm only using Ruby for the web
where most of this stuff is unfortunetly not needed and therefore most of it can be overlooked.

## Symbols and Ranges

_Overview: Symbols are mainly just immutable strings, a lot of times you can replace one for the
other. Know_`to_s`_ and _`to_sym`_. For Range, know that to to initialize, use parenthesis and
about_ `to_a`.

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

Likely ganna quickly go over, don't come up that often at work.
