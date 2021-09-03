---
title: "Ending and Starting"
layout: post
date: 2021-09-03 15:00 +0100
categories: Weeknotes
tags: MSc
---

Today I handed in my dissertation, drawing a line under the past year of work
towards my MSc at the University of Bath. <!--more--> There's a bit of a wait
for the results now, but charging ahead with plans for getting out to Canada.

Just a few stats about my dissertation:
- Roughly 3500 lines of code
- Around 17000 words written, an average of 117 a day
- 97 Experiment runs

I've found a job that will take me out in Vancouver and received an invitation
to apply for the IEC Working Holiday Visa, that's been the other really good
news from this month! I'm filling out my application, once it's in I should
hear back within 12 weeks. Ideally I'll be heading out for good (or at least
the 2 years of the IEC) around mid-November.

## Reflecting on the Bath Computer Science MSc

Bath bills this as a conversion course for those who already have an
undergraduate degree in an unrelated subject and want to convert to Computer
Science. For someone with a humanities background but two years of technical
experience it was very well pitched. Overall it was a great experience, with
some fantastic tutors and important lessons. I felt reasonably ahead at the
beginning thanks to a few coding MOOCs I'd
taken[^1]
, but no-one seemed to be really struggling to keep up with
the material. It doesn't have all of the in depth materials that you would see
in a three year undergraduate course. We had some fantastic training on the
fundamentals that really boosted me from where I was previously. I feel
confident in learning any language I need to, and definitely in calling myself
a developer or a programmer, although I still have a lot to learn and a long
way to go.

What was missing:
- Data structures and algorithms. Considering the expectations of interviewers
    revolves around whiteboard exercises and solving Leetcode style problems
    this was the one aread that was completely missing. However, I would
    defend its exclusion. A year really isn't that long to squeeze in that much
    content, and DSA patterns are really suitable for self study once you
    have other principles learned.
- Operating systems. We learnt a lot at the foundational (Turing Machine,
    Lambda-calculus) level, and a lot more about the higher abstraction levels,
    but not much about the middle levels of Operating Systems or the Von
    Neumann architecture. Again this isn't too much of a loss, it's just what's
    sacrificed with the shorter timescale.

What was great:
- Foundations of computation. The education on this truly foundational part
    of the course was really well delivered. The journey from finite state
    machines to Turing machines and the halting problem was really well led.
    Definitely a lot of important things I wouldn't have learned otherwise.
- Functional programming. Similarly this course was really good at introducing
    us to a paradigm we need to know about, and probably wouldn't have sought
    out independently. I'm getting more curious about functional programming,
    while maybe not as fully converted as some others from the course (looking
    at my pal Vlad here) I definitely see the utility. It creates far cleaner,
    faster program flows when used properly.
- Reinforcement learning. This was another really well put together course on
    an interesting subject. It helped pierce the veil for me around RL and
    machine learning in general. Definitely helped me understand the roots
    of the discipline, the mathematics that underpins recent developments,
    and a vague sense of where the field is headed. My dissertation ended up
    in this area too and, while I'm not sure I want to look at an artificial
    neural network for a little while, it was a great experience putting it
    into practice.

## What else is going on

I had a bunch of setbacks and steps forward again with my dissertation. I
stopped writing up these weeknotes for the past month while I just had my
head down, but now hopefully they'll help me keep a bit more structure as I
go forward.

I've been getting pretty [Rust](https://www.rust-lang.org/) curious. Started
reading [*Rust in Action*](https://www.manning.com/books/rust-in-action) during
my evenings, it's fantastically written. Trying to play around with the
language, need to find a project to apply it to. Part of my dissertation
was writing a Tetris environment for reinforcement learning, but the whole
thing was written in Python. I Cythonized the core loop for a bit of a speed
up but its still laughably slow compared to what you can do in C or Rust, so
that might be a fun thing to rewrite.

# Reading List
- [What science can tell us about C and C++'s security](https://alexgaynor.net/2020/may/27/science-on-memory-unsafety-and-security/)
- [It looks like a product but is secretly a subscription](https://calpaterson.com/printers.html)
- [Make your own text prompt AI-generated art](https://twitter.com/hillelogram/status/1422603763009851398?s=20)
- [Apple’s New ‘Child Safety’ Initiatives, and the Slippery Slope](https://daringfireball.net/2021/08/apple_child_safety_initiatives_slippery_slope)
- [Rust in Action](https://www.amazon.co.uk/Rust-Action-Tim-McNamara/dp/1617294551)
- [For programmers, remote working is becoming the norm](https://www.economist.com/graphic-detail/2021/08/11/for-programmers-remote-working-is-becoming-the-norm)
- [The Impossibility of Automating Ambiguity](https://direct.mit.edu/artl/article/27/1/44/101872/The-Impossibility-of-Automating-Ambiguity)
- *Identity*, Milan Kundera
- [The Ides of August](https://www.sarahchayes.org/post/the-ides-of-august)
- [Let us not praise famous women](https://debuk.wordpress.com/2021/07/31/let-us-not-praise-famous-women/)
- [Benefits of not using an IDE](https://alexander-hansen.dev/blog/benefits-of-not-using-an-ide)
- [I give you feedback on your blog post draft but you don't send it to ](https://mango.pdf.zone/i-give-you-feedback-on-your-blog-post-draft-but-you-dont-send-it-to-me)
- [How Discord Stores Billions of Messages](https://blog.discord.com/how-discord-stores-billions-of-messages-7fa6ec7ee4c7)
- [China’s top court takes aim at ‘996’ overtime culture in blow to tech groups](https://www.ft.com/content/a794faf1-2ee9-4d19-abc6-72620227396c)
- [Disaster Limbo](https://hot-take.ghost.io/disaster-limbo/)
- [Some reasons to measure](https://danluu.com/why-benchmark/)
- [Motherhood at the End of the World](https://www.theparisreview.org/blog/2021/09/01/motherhood-at-the-end-of-the-world/)
- [Operations is not Developer IT](https://matduggan.com/operations-is-not-developer-it/)

[^1]: [CS50](https://cs50.harvard.edu/) was the main one I recommend to
    anyone else interested in the jump, and a really important follow up is
    [Missing Semester](https://missing.csail.mit.edu/) for all of the skills that
    get glossed over by other courses.
