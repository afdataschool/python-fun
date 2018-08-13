---
title: "Design recipe"
teaching: 30
exercises: 30
questions:
- "fix me"
objectives:
- "fix me"
keypoints:
- "fix me"
---

## Design Recipe

This design recipe can be applied to functions in any language:

> ## DESIGN RECIPE
> 1. **Signature**: this decribes how many inputs and outputs our function has, and their type.
> 2. **Purpose**: a short, succinct description of the task (one line max)
> 3. **Stub**: puts names to the inputs and outputs of the function
> 4. **Examples**: demonstrates how you expect your function to behave in difference scenarios.
>
> We will go through each of these steps in turn below.
{: .callout}

## Signature
  
The signature formalises the process of describing our function's inputs and outputs. Let's consider our DNA example again:

> The component acids that form DNA are often represented as 'A', 'T', 'G', and 'C'. The amount of 'G' and 'C' in 
> a DNA sequence tends to be organism specific. You've received some sequence data from a service provider,
> and as a simple test of contamination you want to check its GC ratio.
{: callout}

We might write:

`compute_gc: String -> Float`

Here, `compute_gc` is the name we choose to give our funtion. Following the name, we describe a single input, of type `String`. The arrow points to the output data, of type `Float`.

> ## Antibiotic signature
> Fill in the blanks to complete this signature:
>
> 'Antibiotics are sometimes tested by 'dropping' a measured dose onto the middle of a petri dish that is 
> covered in a bacterial 'lawn'. Resistance is measured as the area of the disk still covered by bacteria 
> after 2 days. Bacterial death spreads out from the antibiotic drop creating a perfect bacteria-free central 
> disk. You've recorded the diameter of several hundreds of test spots, with three replicates per plate. You want to find 
> the average measure of resistance.' 
>
> ~~~
> mean_resistance: Float ____ ____ -> ____
> ~~~
> {: .source}
{: .challenge}

> ## Field data signature
> Let's revisit our email: 
>
> "The field data is back from the trial, but unfortunately I'm having a lot of 
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


## Purpose

This one sounds deceptively easy: in one sentence (say, 80 characters max), describe what your function does.

> Purpose statement guidelines:
> * Avoid repeating the word problem. It likely contains extra 'tasks' that you're function *doesn't* or *shouldn't* actually do.
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

Here, we sketch out our actual function, giving names to the input and output data. Soon, you will see how to do this in
Python 3 notation, however for now, let's copy the format of our signature:

If our field trial signature is:

`convert_date: String String String -> String`

Then our stub might become:

`convert_date: Day Month Year -> Date`

> ## Stub rules
> * must have the same number of inputs and outputs as our signature
> * must have the same function name as our signature
> * names given to each input are the **argument variables** we pass to our function, and can be used inside our function
> * names given to each output are the **return variables**
{: .callout}


> ## DNA Stub
> Given the stub
>
> `compute_gc: String -> Float`
> 
> write the corresponding stub
{: .challenge}

> ## Antibiotic Stub
> Given the signature:
>
> `mean_resistance: Float Float Float -> Float`
>
> which of the following is a valid stub? Which is the best stub? What would you improve?
> 1. v1 v2 v3 -> return
> 2. mean_resistance: diameter_one diameter_two diam_3 -> resistance
> 3. mean_res: diam_1 diam_2 diam_3 -> lawn_area
> 4. mean_resistance: diameter diameter diameter -> lawn_area
> 4. mean_resistance: d1 d2 d3 -> Float
{: .challenge}


## Examples

Examples are the most important part of your function design recipe, and often the most overlooked! If you can master the art of writing good examples, then you will be able to write code that works, is easy to read, and is easy to debug.

Example guidelines
 * choose 3 or 4 well-thought out examples
 * try and find 'boundary' conditions.
 * for now, design examples that are **meant** to work, rather designing examples to break your code. 

> ## Boundary conditions
> 
> What are boundary conditions? It's often easy to write code that works for the main way you expect people to use your function.
> But what about situations you haven't thought of? Or that are unusual. Let's consider our DNA example. We might expect 
> most DNA input sequences to look something like:
> `ATCCTGTTTAGGATCGT`
> Some example 'boundaries' might include:
> * `T` - only one base in the sequence
> *  `GGGGGGGGGG` - all bases in the sequence identical
> * `TGgggTCaGtnAAa`- sequence contains mix of capital and lower case letters, or 'n'
{: .callout}

Working out your boundary conditions, and including them as examples in your function documentation, is what really defines how your function should behave. Not only does it help you write the function, it also tells anyone else who uses it or reads it exactly what to expect. 

In our 'generic' function design recipe, you can formulate your examples just like your signature and stub:

`compute_gc: T -> 0.0`
`compute_gc: GGGGGGGGG -> 100.0`

> ## DNA
>
> write an example based on the boundary condition `TGgggTCaGtnAAa`
{: .challenge}

> ## Boundaries and examples
> 
> Write out boundary conditions and examples for the field trial and antibiotic exercises. 
{: .challenge}


{% include links.md %}

