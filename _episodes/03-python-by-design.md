---
title: Creating Functions
teaching: 30
exercises: 0
questions:
- "How can I define new functions?"
- "What's the difference between defining and calling a function?"
- "What happens when I call a function?"
objectives:
- "Define a function that takes parameters."
- "Return a value from a function."
- "Test and debug a function."
- "Set default values for function parameters."
- "Explain why we should divide programs into small, single-purpose functions."

keypoints:
- "Define a function using `def function_name(parameter)`."
- "The body of a function must be indented."
- "Call a function using `function_name(value)`."
- "Numbers are stored as integers or floating-point numbers."
- "Variables defined within a function can only be seen and used within the body of the function."
- "If a variable is not defined within the function it is used, Python looks for a definition before the function call"
- "Use `help(thing)` to view help for something."
- "Put docstrings in functions to provide help for that function."
- "Specify default values for parameters when defining a function using `name=value` in the parameter list."
- "Parameters can be passed by matching based on name, by position, or by omitting them (in which case the default value is used)."
- "Put code whose parameters change frequently in a function, then call it with different parameter values to customize its behavior."
---

So, we know conceptually how to design a function, but how do we put this into Python? What is the Python syntax?

Let's start by defining a function `fahr_to_celsius` that converts temperatures
from Fahrenheit to Celsius.

> ## Fahr_to_celsius
> 1. Write out the signature, purpose, stub, and examples.
> 2. Work out some code that performs the calculation.
> 3. Next, we will put this all together into a function!
{: .challenge}

~~~
def fahr_to_celsius(temp_fahr):
    temp_cels = (temp - 32) * (5/9)
    return(temp_cels)
~~~
{: .language-python}


The function definition opens with the keyword `def` followed by the
name of the function (`fahr_to_celsius`) and a parenthesized list of parameter names (`temp`). The
body of the function --- the
statements that are executed when it runs --- is indented below the
definition line.  The body concludes with a `return` keyword followed by the return value.

When we call the function,
the values we pass to it are assigned to those variables
so that we can use them inside the function.
Inside the function,
we use a to send a result
back to whoever asked for it.

Let's try running our function.

~~~
fahr_to_celsius(32)
~~~
{: .language-python}

This command should call our function, using "32" as the input and return the function value.

In fact, calling our own function is no different from calling any other function:
~~~
print('freezing point of water:', fahr_to_celsius(32), 'C')
print('boiling point of water:', fahr_to_celsius(212), 'C')
~~~
{: .language-python}

~~~
freezing point of water: 0.0 C
boiling point of water: 100.0 C
~~~
{: .output}

We've successfully called the function that we defined,
and we have access to the value that we returned.

> ## The Python Stub
> Now we know the format of a Python function, we can write out the signature and stub more meaningfully.
> Start your signature as a comment (some languages require a signature as part of the function definition; for 
> complicated reasons Python does not. For now, I think it is helpful to include a signature comment.)
> 
> `# fahr_to_celsius: Float -> Float`
> 
> For our stub, we can sketch out the actual function:
> 
> ~~~
> def fahr_to_celsius(temp_fahr):
>      ....
>      return(temp_celsius)`
> ~~~
> {: .language_python}
>
> putting it together, we have:
> 
> ~~~
> # fahr_to_celsius: Float -> Float
> def fahr_to_celsius(temp_fahr):
>      ....
>      return(temp_celsius)`
> ~~~
> {: .language_python}
{: .callout}

## Composing Functions

Now that we've seen how to turn Fahrenheit into Celsius,
we can also write the function to turn Celsius into Kelvin:

One way to do this is:

~~~
def celsius_to_kelvin(temp_c):
    return(temp_c + 273.15)

print('freezing point of water in Kelvin:', celsius_to_kelvin(0.))
~~~
{: .language-python}

~~~
freezing point of water in Kelvin: 273.15
~~~
{: .output}

Note that here, we don't 'save' the return value in a variable before the 
return statment; we just include the calculation as part of the return statement. Why would / wouldn't you do this?

What about converting Fahrenheit to Kelvin?

> ## Fahrenheit to Kelvin
> Write out the signature and stub for this function using Python notation.
> Now, fill in the body. Can you do this without using the formula?
{: .challenge}

We can utilise the two functions we have already created:

~~~
def fahr_to_kelvin(temp_f):
    temp_c = fahr_to_celsius(temp_f)
    temp_k = celsius_to_kelvin(temp_c)
    return(temp_k)

print('boiling point of water in Kelvin:', fahr_to_kelvin(212.0))
~~~
{: .language-python}

~~~
boiling point of water in Kelvin: 373.15
~~~
{: .output}

This is our first taste of how larger programs are built:
we define basic operations,
then combine them in ever-large chunks to get the effect we want.

Real-life functions will usually be larger than the ones shown here --- typically half a dozen
to a few dozen lines --- but they shouldn't ever be much longer than that,
or the next person who reads it won't be able to understand what's going on.


## Documenting

If the first thing inside a Python function is a string that isn't assigned to a variable,
but rather attached to the function as its documentation:

~~~
def fahr_to_celsius(temp_fahr):
    '''Converts temperature in fahrenheit to temperature in celsius'''
    temp_cels = (temp - 32) * (5/9)
    return(temp_cels)
~~~
{: .language-python}

What a great place to put your purpose statement! 
This has the added benefit that we can now ask Python's built-in help system to show us
the documentation for the function:

~~~
help(fahr_to_celsius)
~~~
{: .language-python}

~~~
Help on function fahr_to_celsius in module __main__:

fahr_to_celsius(fahr_temp)
    Converts temperature in fahrenheit to temperature in celsius. 
~~~
{: .output}

A string like this is called a [docstring]({{ page.root }}/reference/#docstring).

## Doctests

There is a super-neat (if somewhat unpopular!) way of including examples in your
Python documentation:

~~~
import doctest
def fahr_to_celsius(temp_fahr):
    '''Converts temperature in fahrenheit to temperature in celsius.
    >>> fahr_to_celsius(52.0)
    11.1
    >>> fahr_to_celsius(0)
    -17.8'''
    
    temp_cels = (temp - 32) * (5/9)
    return(temp_cels)

doctest.testmod()
help(fahr_to_celsius)
~~~
{: .language-python}

~~~
Help on function fahr_to_celsius in module __main__:

fahr_to_celsius(temp_fahr)
    Converts temperature in fahrenheit to temperature in celsius.
    >>> fahr_to_celsius(52.0)
    11.1
    >>> fahr_to_celsius(0)
    -17.8
~~~
{: .output}

> ## fahr_to_celsius
> Do your examples exactly match your function? Do they match mine?
> Assuming you've used the examples above, modify your function to match the examples.
{: .challenge}

> ## Change the body, not the examples!
> You've already thought a lot about how you want your function to behave. Using documentation-driven-development (or test-driven development), you've already defined 'correct'. 
> If you get an unexpected result, or a result that is not *quite* what you expect, don't cheat and change your documentation.
> As we have seen, functions often rely on other functions... if you redefine what you *want* your function to do on the fly, 
> you are likely to break other parts of your code. Instead, keep working on the logic of your function until it exactly 
> matches your examples.
{: .callout}

> ## fahr_to_celsius
> In the last exercise, you modified your function body so that only one decimal place was returned. What if you want to be 
> able to 'choose' every time you call your function, how many decimal places to include? 
> 1. Using Python notation, write out the signature, stub, purpose, and examples for your function.
> 2. Fill out the body of your function.
{: .challenge}

## Defining Defaults

let's revisit the `round()` function:

~~~
pi = 3.14159265359
round(pi)
round(pi, 3)
help(round)
~~~
{: .language_python}

We can call the function `round()` with either one or two arguments; the second argument (ndigits) is optional, and defaults to 0. How do we set up defaults in our own functions?

> # defaults
> write out the fahr_to_celsius signature, stub, and purpose, so the number of decimal places is also a function parameter
{: .challenge}

~~~
def fahr_to_celsius(temp_fahr, n=1):
    '''Converts temperature in fahrenheit to temperature in celsius.
    >>> fahr_to_celsius(52.0)
    11.1
    >>> fahr_to_celsius(0)
    -17.8'''
    temp_cels = round((temp - 32) * (5/9), n)
    return(temp_cels)

fahr_to_celsius(52)
fahr_to_celsius(52, 8)
~~~
{: .language-python}


The key change is that the second parameter is now written `n=1`
instead of just `n`.


> ## Return versus print (again!)
>
> Note that `return` and `print` are not interchangeable.
> `print` is a Python function that *prints* data to the screen.
> It enables us, *users*, see the data.
> `return` statement, on the other hand, makes data visible to the program.
> Let's have a look at the following function:
>
> ~~~
> def add(a, b):
>     print(a + b)
> ~~~
> {: .language-python}
>
> **Question**: What will we see if we execute the following commands?
> ~~~
> A = add(7, 3)
> print(A)
> ~~~
> {: .language-python}
>
> > ## Solution
> > Python will first execute the function `add` with `a = 7` and `b = 3`,
> > and, therefore, print `10`. However, because function `add` does not have a
> > line that starts with `return` (no `return` "statement"), it will, by default, return
> > nothing which, in Python world, is called `None`. Therefore, `A` will be assigned to `None`
> > and the last line (`print(A)`) will print `None`. As a result, we will see:
> > ~~~
> > 10
> > None
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

> ## Selecting Characters From Strings
>
> If the variable `s` refers to a string,
> then `s[0]` is the string's first character
> and `s[-1]` is its last.
> Write a function called `outer`
> that returns a string made up of just the first and last characters of its input.
> Start with the signature, stub, purpose, and examples. 
> A call to your function should look like this:
>
> ~~~
> print(outer('helium'))
> ~~~
> {: .language-python}
>
> ~~~
> hm
> ~~~
> {: .output}
{: .challenge}



> ## Variables Inside and Outside Functions
>
> What does the following piece of code display when run --- and why?
>
> ~~~
> f = 0
> k = 0
>
> def f2k(f):
>   k = ((f-32)*(5.0/9.0)) + 273.15
>   return k
>
> f2k(8)
> f2k(41)
> f2k(32)
>
> print(k)
> ~~~
> {: .language-python}
>
> > ## Solution
> >
> > ~~~
> > 259.81666666666666
> > 287.15
> > 273.15
> > 0
> > ~~~
> > {: .output}
> > `k` is 0 because the `k` inside the function `f2k` doesn't know
> > about the `k` defined outside the function.
> {: .solution}
{: .challenge}

> ## Mixing Default and Non-Default Parameters
>
> Given the following code:
>
> ~~~
> def numbers(one, two=2, three, four=4):
>     n = str(one) + str(two) + str(three) + str(four)
>     return n
>
> print(numbers(1, three=3))
> ~~~
> {: .language-python}
>
> what do you expect will be printed?  What is actually printed?
> What rule do you think Python is following?
>
> 1.  `1234`
> 2.  `one2three4`
> 3.  `1239`
> 4.  `SyntaxError`
>
> Given that, what does the following piece of code display when run?
>
> ~~~
> def func(a, b=3, c=6):
>   print('a: ', a, 'b: ', b, 'c:', c)
>
> func(-1, 2)
> ~~~
> {: .language-python}
>
> 1. `a: b: 3 c: 6`
> 2. `a: -1 b: 3 c: 6`
> 3. `a: -1 b: 2 c: 6`
> 4. `a: b: -1 c: 2`
>
> > ## Solution
> > Attempting to define the `numbers` function results in `4. SyntaxError`.
> > The defined parameters `two` and `four` are given default values. Because
> > `one` and `three` are not given default values, they are required to be
> > included as arguments when the function is called and must be placed
> > before any parameters that have default values in the function definition.
> >
> > The given call to `func` displays `a: -1 b: 2 c: 6`. -1 is assigned to
> > the first parameter `a`, 2 is assigned to the next parameter `b`, and `c` is
> > not passed a value, so it uses its default value 6.
> {: .solution}
{: .challenge}

> ## The Old Switcheroo
>
> Consider this code:
>
> ~~~
> a = 3
> b = 7
>
> def swap(a, b):
>     temp = a
>     a = b
>     b = temp
>
> swap(a, b)
>
> print(a, b)
> ~~~
> {: .language-python}
>
> Which of the following would be printed if you were to run this code?
> Why did you pick this answer?
>
> 1. `7 3`
> 2. `3 7`
> 3. `3 3`
> 4. `7 7`
>
> > ## Solution
> > `3, 7` is correct. Initially `a` has a value of 3 and `b` has a value of 7.
> > When the swap function is called, it creates local variables (also called
> > `a` and `b` in this case) and trades their values. The function does not
> > return any values and does not alter `a` or `b` outside of its local copy.
> > Therefore the original values of `a` and `b` remain unchanged.
> {: .solution}
{: .challenge}


{% include links.md %}


