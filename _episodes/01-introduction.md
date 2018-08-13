---
title: "Word problems"
teaching: 30
exercises: 30
questions:
- "How do I get from a description of a problem, to a code solution?"
objectives:
- "Extract coding task from word problem"
- "Identify input and output data"
- "Describe a coding task's main function"
- "Formulate useful examples of the task"
keypoints:
- "Functions operate on input data, producing output data"
- "Identifying and describing the data task is the biggest challenge in writing functions"
- "A systematic design recipe will help you write elegant functions from the get-go!"
---

## The black-box function

Functions are at the heart of programing; they are the machines that do work. A function is a bit like a black box; you give it some input, it does some magic, and spits out some output. You've seen this is action already:

~~~
first_name = 'Kerensa'
len(first_name)
~~~
{: .language-python}

~~~
7
~~~
{: .output}

Here, we've called the fuction `len()`, with the input data `first_name`, and recieved some output data `7`. We don't see the internal workings or calculations of the function, len() is essentially a black box that does some processing.

> ## Input and output data
> Describe the input and output of the following build in fuctions:
> 1. round()
> 2. str()
> 3. print() 
>
> What is the **type** of each input and output?
{: .challenge}


> ## Documentation driven development
> Beginner (and often even advanced!) coders often start writing a new function by working out the logic inside
> the black box. This path is hard and bug-prone! For now, let's focus on defining and describing what we want
> our function to do. Once that is crystal clear, working out the nuts and bolts inside the black box is much
> easier.
{: .callout}

## Words to functions

Often, the hardest part of writing your own functions, is working out *what* to write. You're given a description of a task someone wants you to do, and you need to turn this into language that the computer understands. Let's try some word problems. A colleague sends you an email asking:

"The field data is back from the trial, but unfortunately I'm having a lot of trouble loading it into the software because the assistant recorded the dates using the month's name, and it wants dates formatted like 2018-03-02, 2018-06-04, etc. Do you think you could write me a quick script to help me out?" 

I always start by identifying the data in the description. Here, the output data is a string, formatted like yyyy-mm-dd. As input data, we have the names of months, also a string. Presumably, based on the output, we are given year and day as well.

> ## Data discussion
> Is this data description complete?
> Are we given enough information to write the program?
{: .discussion} 

After I've worked out the data (it can help to use a highlighter to start with!), I then work out what the actual task I'm being asked to do is. Here, I might say "Reformat dates containing month names to a numerical description e.g. yyyy-mm-dd."

> ## Antibiotics
> 
> Antibiotics are sometimes tested by 'dropping' a measured dose onto the middle of a petri dish that is 
> covered in a bacterial 'lawn'. Resistance is measured as the area of the disk still covered by bacteria 
> after 2 days. Bacterial death spreads out from the antibiotic drop creating a perfect bacteria-free central 
> disk. You've recorded the diameter of several hundreds of test spots, with three replicates per plate. Find 
> the average measure of resistance. 
{: .challenge}

> ## DNA
>
> The component acids that form DNA are often represented as 'A', 'T', 'G', and 'C'. The amount of 'G' and 'C' in 
> a DNA sequence tends to be organism specific. You've got received some sequence data from a service provider,
> and as a simple test of contamination you want to check its GC ratio.
{: .challenge}

> ## Design Recipe
> As you can see from the exercises above, there are often ambiguities involved in interpreting a problem. 
> Choices need to be made, often regarding:
> * the kind of input data your function will accept, and output data it will generate
> * the function's 'scope'; will it do everything in the description, or a smaller implied task?
>
> There is often not a 'right' or 'wrong' answer to these questions. However, you need answers in order to 
> define whether your function is working correctly, and in fact to know what you want to code in the first 
> place!
> This is where a 'Design Recipe' can help, by forcing you to answer these questions before you write code.
>
> **DESIGN RECIPE**
> 1. **Signature**: this decribes how many inputs and outputs our function has, and their type.
> 2. **Purpose**: a short, succinct description of the task (one line max)
> 3. **Stub**: puts names to the inputs and outputs of the function
> 4. **Examples**: demonstrates how you expect your function to behave in difference scenarios.
> We will go through each of these steps in turn below.
{: .callout}

## Signature
  
The signature formalises the process of describing our function's inputs and outputs. Taking the 
'DNA' example above, we might write:

`compute_gc: String -> Float`

Here, `compute_gc` is the name we choose to give our funtion. Following the name, we describe a single input, of type `String`. The arrow points to the output data, of type `Float`.

> ## Antibiotic signature
> Given your answers to the antibiotic word problem above, fill in the blanks to complete this signature:
>
> ~~~
> mean_resistance: Float ____ ____ -> ____
> ~~~
> {: .source}
{: .challenge}

> ## Field data signature
> Let's revisit our email: "The field data is back from the trial, but unfortunately I'm having a lot of 
> trouble loading it into the software because the assistant recorded the dates using the month's name, and 
> it wants dates formatted like 2018-03-02, 2018-06-04, etc. Do you think you could write me a quick script 
> to help me out?
> 
> Which of the following would make good signatures? (there may be more than one answer)
> 1. `convert_date: Int String Int -> Int`
> 2. `convert_date: Int String Int -> String`
> 3. `convert_date: Day Month Year -> yyyy-mm-dd`
> 4. `convert_date: String -> String`
> 5. `convert_date: String String String -> Int Int Int`
{: .challenge}

> ## DNA signature.
>
> Formalise a signature for your DNA word problem: 
>
> 'The component acids that form DNA are often represented as 'A', 'T', 'G', and 'C'. The amount of 'G' 
> and 'C' in a DNA sequence tends to be organism specific. You've got received some sequence data from 
> a service provider, and as a simple test of contamination you want to check its GC ratio.
{: .challenge}

## Purpose

This one sounds deceptively easy: in one sentence (say, 80 characters max), describe what your function does.

> Purpose statement guidelines:
> * Avoid repeating the word problem. It likely contains extra 'tasks' that you're function *doesn't* actually do.
> * Don't repeat info that is in the signature. There is no need for the name of the function, or a description
> of its inputs and outputs.
> * Keep it as generic as possible. If it calculates the area of a rectangle, say it calculates the area of a rectangle. Don't say, it gives the area of a Boorowa field plot. 
> * Try and word it so any colleague in Agriculture and Food would understand it.
{: .callout}

Let's return again to our field data example:

'The field data is back from the trial, but unfortunately I'm having a lot of trouble loading it into the software because the assistant recorded the dates using the month's name, and it wants dates formatted like 2018-03-02, 2018-06-04, etc. Do you think you could write me a quick script to help me out?'

We've already defined our signature:

`convert_date: String String String -> String`

(note the clarity already given by the signature).

A purpose statement might be:

**"Makes the date format yyyy-mm-dd from separate day, month, and year observations"**

> ## DNA purpose statement
> 
> Which of the following is the best purpose statement for our DNA example?
>
> 1. Takes a string of DNA characters and returns the GC percentage as a float.
> 2. Calculates how many bases are in a DNA sequence, then calculates how many GC bases are in the same sequence, then divides the GC by the DNA to find the ratio.
> 3. Calculates the average GC content of a DNA sequence.
> 4. Calculates the proportions of (G + C) in any given string. 
{: .challenge}

> ## Antibiotic purpose statement
>
> Given your word problem and signature, write a purpose statement for the antibiotic exercise:
>
> 'Antibiotics are sometimes tested by 'dropping' a measured dose onto the middle of a petri dish that is
> covered in a bacterial 'lawn'. Resistance is measured as the area of the disk still covered by bacteria
> after 2 days. Bacterial death spreads out from the antibiotic drop creating a perfect bacteria-free central
> disk. You've recorded the diameter of several hundreds of test spots, with three replicates per plate. Find
> the average measure of resistance.'
{: .challenge}

## Stub

Here, we sketch out our actual function, giving names to the input and output data. This is a lot like our
signature, however here we start to use proper Python 3 notation: 

Starting from the Field Trial signature, `convert_date: String String String -> String`, the 'logic' of 
our stub becomes `convert_date: Day Month Year -> Date`.

In Python function definition notation, we write:
~~~
def convert_date(day, month, year):
    #function body	
    return(date)
~~~
{: .language-python}

To keep our design process all together, let's add in the signature and purpose statement:
~~~
#convert_date: String String String -> String
def convert_date(day, month, year):
    """Makes the date format yyyy-mm-dd from separate day, month, and year observations"""
    #function body
    return(date)
~~~
{: .language-python}
> ## Antibiotic Stub
> Given the signature
{: .challenge}

{% include links.md %}

