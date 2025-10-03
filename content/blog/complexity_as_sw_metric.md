+++
title = "Complexity as a Software metric"
date = "2020-07-20T11:46:20+01:00"
tags = ["CI"]
categories = ["metrics"]
banner = "img/banners/maze.jpg"
authors = ["Paul Blay"]
+++

I’ve never been completely sold on Cyclomatic Complexity as a metric, it maps to linearly independent paths through code which may be useful to get an indication on the level of testing an application needs, assuming code coverage is not available (another metric that needs to be treated with caution), but how much value is that? Most applications are multi threaded and do not run in a linear fashion, I’d argue that there’s considerably more value in measuring the readability of code in order to allow people to understand what it does and how to change it. I’ve seen easy-to-read and hard-to-read methods that evaluate to the same value on the Cyclomatic Complexity scale. Perhaps that’s ok and we care about logical complexity, but my (weakly held) strong opinion is that the real value is in ease of human understanding when it comes to code.

Perhaps Cyclomatic Complexity has a place as an indicator of worsening or improving code complexity, but I’m happy to say that I have found something that comes a lot closer to evaluating “can I work out what it’s doing?” type complexity, in my mind at least.

As part of some work that we’re doing on metrics, I had a look into alternative code complexity measure and stumbled upon Cognitive Complexity – a metric that SonarQube, amongst others presumably, can report.

Now before moving on, I’m assuming that there’s little disagreement that “internal code quality” (of which readability is an aspect) is a valuable thing. If not, stop reading and go here: https://martinfowler.com/articles/is-quality-worth-cost.html 

So what is Cognitive Complexity? Other than being obviously how hard something is to get your head around. Well there’s a great whitepaper here, but I’ll try to summarise the content below.

Take a look at these examples from the whitepaper:

![Cyclomatic_complexity](/paulblay-hugo/img/complexity/complexity_1.png)

Which is easier to read and understand? In fact, which is actually more complex and which would need more testing?

Here are the same code snippets measured with the Cognitive Complexity metric:

![Cyclomatic_complexity](/paulblay-hugo/img/complexity/complexity_2.png)

… that’s more like it.

How is this done? There are three basic rules

**Ignore Structures that allow multiple statements to be readably shorthanded into one.**

A good example of this is the breaking up of code into methods to increase readability. As a result, Cognitive Complexity does not increment for methods as Cyclomatic Complexity does.

The aim here is to not penalise good programming practice like an increased number of smaller methods, because it is likely to reduce complexity for a reader.

**Increment when flow-breaking structures are nested**

Nested breaks in flow increase count as a proportion of how deeply they are nested. So a new “if” that is nested 4 deep adds 5 to the complexity score. 1 for the “if” and 4 for the nest level.

This is because it’s intuitively easier to follow a linear list of code breaks than an equally, Cyclomatic Complexity-wise, complicated nested set of code breaks.

**Increment for each break in the linear flow of the code**

Anything that breaks the top to bottom, left to right flow of the code increases Cognitive Complexity, similarly to Cyclic Complexity, but there are some interesting differences.

1. “Catch” is added as a break in flow

2. “Else”, “Elif” and other alternatives to the initial “if” break in flow do increment but not with the same nesting penalty as above, as the nesting complexity is considered paid already at the initial “if”.

3. “Switch” statements only incur a single increment, regardless of cases. Switch statements are considered more understandable then multiple “if”/”else if” blocks.

4. Repeating logical comparisons with the same logic operator only increment complexity once. This is because it’s fairly similar effort to understand both of the following lines

``` a && b ``` 

``` a && b && c && d ```

but much harder to understand a statement with mixed logical operators

``` a || b && c || d ```

5. Recursion is the one exception to the “don’t increment for methods” rule

6. “goto”, “break” and “continue” increase complexity, but no other jumps are. e.g. an early “return” is considered to make code clearer so is ignored.

The white paper referenced above is not long and I highly recommend reading it, but I hope that this is a useful summary (if nothing else, writing this caught a couple of mis-conceptions I’d made from just reading the paper).

Thanks for reading!