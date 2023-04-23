---
layout: post
title: "Best Practices for Software Engineering (IMHO)"
date: 2023-04-22 10:43:00 +0700
categories: technical
tags: software-engineering swe productivity
---

I feel like I've been learning a lot over the past 9 months that I've been 
working full time as an SDE. I want to get some of that understanding down
in an open place. Here's a doc, that will hopefully evolve over time, on 
some best practices that I've come to know about since working. 
<!--more-->

This is going to be a list of topics that I think are really core to being 
effective when working in a team on software projects that are intended to 
have a lifetime in the years or decades. Mostly this is from what I've 
learned at work, and there's a large amount of overlap with the reading that 
I've done, particularly with Titus Winters's great book [*Software Engineering 
at Google*](https://www.amazon.ca/Software-Engineering-Google-Lessons-Programming/dp/1492082791).

I really enjoyed the definition in there of Software Engineering being 
"programming over time". The goal is not just to produce an implementation, 
but to create software that will last and evolve over the time you need it to.
That's going to vary from company to company and project to project, and 
that's fine! 

## Best practices (that I know about)

I'm prefacing this with the disclaimer that these are all my relatively 
naive opinions and understandings. I also think these mostly apply in large 
organisations, where you're working collaboratively with other engineers 
over long timescales. All of these make delivering software in those 
conditions easier, but they probably don't make sense as a startup or an 
indie creator. The same problems that each of these ideas solve or mitigate 
will emerge, but they probably won't be as big of a deal depending on your
scale. 

### Build Systems

Build systems solve the problem of software packages relying on each other. 
A simple example of this is writing a simple Python script, and then trying
to run that on another machine. This is very easy when its a simple script,
with no dependencies, that uses features that have been stable for a long time.
But what if the script uses features only in Python 3.10, and it also relies
on packages like `numpy` or `pandas`. It starts to build up a graph of 
dependencies, and each of these dependencies will have dependencies of their 
own, and so on, until you reach `libc` and sys-calls. 

I'm putting build systems right at the top because they're so key to writing
software that runs on any machine other than your own. A good build system 
should handle:
- Package versioning
- Dependency graphs
- Build scripts (that include unit tests)

It should be:
- Reproducible: the same dependency graph builds reliably. This essentially
    means that the system is determinstic taken as a whole, there's no 
    randomness in the "will it work/won't it" when using the same "build".
- Declarative: you should be able to specify system requirements through a 
    config file or set of configs. This means that the "build" can be 
    replicated without sending an image of the entire system (as something
    like docker does). You can send a lightweight text file and replicate 
    a system state. 

I'm incredibly lucky to work at a place that has a long experience of working 
with build systems. Amazon (like other 10k+ engineering orgs) has had to 
invest heavily in its build infrastructure so engineers can be productive. 
If I wasn't working at somewhere with such a strong existing solution for this 
issue, I'd be learning [Nix](https://nixos.org/) - and I probably will one 
day. 

Build systems should also ideally be fast! The longer an engineer is waiting
for things to build, the slower their feedback loops, and in general, the 
shorter my feedback loop when working, the quicker I can get something done. 

### Pipelines (CI/CD) 

Pipelines are a pretty well discussed topic by now. 

### Testing 

## Individual best practices 

This is a section on individual best practices. I think these are separate 
enough from the practices of how to work as part of a team over a long 
timescale. This is about being the best developer you can be. 

### Know your tools (editing and reading code)

This element I think is universal. Tools should help you work, and get out
of the way. The primary interface for programming is text. The tools you 
use to read, comprehend, and edit that text are key. It should be a buttery
smooth experience for you to hop around a codebase. Your IDE should conform 
to how you like to work, and you should be able to customise it to extend 
its abilities. 

This is something that [The
Primeagen](https://www.youtube.com/watch?v=bdumjiHabhQ) has really influenced
me on, but this is common with any practice. You should know your tools 
really well, and there's no tool more important in Software than text 
manipulation tools.

IDEs and editors like Vim/Emacs are the core part of this, but I'm not even
talking exclusively about these. Unix tools like grep, ripgrep, awk, sed, sort, 
all of these should be at your fingertips too. My editing is mostly done in
VSCode and Neovim. I use Vim bindings in VSCode, and the benefit of learning
some key movement bindings is that everything feels smoother. The ideal 
state of code editing is where you can edit as fast as you can think. I 
definitely believe that Software Engineering is not about typing, I know the 
majority of the work and understanding should be done before you're setting 
things down in an editor, but there is a huge advantage to being fast when 
you are making changes. You don't have to disrupt your chain of thought with 
a long winded "how should I do that" sidetrack. You can have a little blur at
the keys and your change is already made. Most developers aren't quicking 
between windows on their screen, they're using Alt-tab to shift focus and 
keep their working memory on the task at hand. The more your tools become 
muscle memory, the more they fade into the background. It's like driving, 
changing gears, or putting on your windshield wipers when it rains, all of 
that should be ingrained for you to be able to focus on reacting to the road
around you. 

The other way this is key is in reading code. You should have shortcuts in your
IDE to hop to definitions. You should know how to quickly look up strings in
your codebase, whether that's
[telescope](https://github.com/nvim-telescope/telescope.nvim) in nvim, or 
cmd + shift + f in VSCode. You can learn a lot about how some code is used 
with just grep. 





### Little scripts 

One area where I think 
generative LLMs are incredibly useful is in getting over the learning curve 
for little scripts that help you get your work done. 