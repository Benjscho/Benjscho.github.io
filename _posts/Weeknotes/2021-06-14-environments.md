---
layout: post
title: "Environments"
date: 2021-06-14 20:30 +0100
categories: Weeknotes
tags: MSc
---

I just got back from seeing my Grandparent's on my Dad's side for the first
time in maybe a year and a half.  <!--more--> It was a very hot weekend, very
good to see them. They're getting on now, and as always the most important
thing in life is to spend time with the people you care about.

While we were driving back something awful happened in the village. The social
centre burned down. It housed a community pub, the post office, provided a
rentable space to local groups, provided part of the heart of the village.
Thinking about environments as a result of all of this. What I'm lucky to be
in, where I would like to be, the things we build and ways in which they slowly
or suddenly fall apart. Not thinking anything interesting about them, just
feels like it's weighing on my mind.

I skipped the weeknotes last week, popped up to London to see some friends.  So
so nice to give them a hug, have a beer, share dinner. I've been missing that
most out in the countryside.

# Tetris and my Dissertation

I'm working on the environment for my dissertation experiments at the moment.
It's a simplified version of Tetris where you indicate the piece orientation
and column in order to drop it, essentially shortening and removing the
trajectory, and allowing you to apply learning at a quicker rate. There are
some other methods of reinforcement learning I've heard about more recently
that seem like they might be promising for the full trajectory version but
I don't think I'm in the place to try out.

In particular ["Exploration by Random Network
Distillation"](http://arxiv.org/abs/1810.12894) sounds like it might be
applicable? I'm reasoning that the task of exploration in a full trajectory
based game of Tetris, where the reward is only gained by clearing a row, this
isn't too dissimilar to Montezuma's revenge where you also have a complex
sequence of actions that have to occur before receiving any reward.  This might
be something to try out, but it sounds pretty high risk in terms of achieving
results, so I'm going to work on the simpler goals from my project plan first.
I have a similar plan with Monte-Carlo Tree Search strategies which would
probably work, but might have a lot of awkward engineering practicalities that
would prevent it. A lot of the excellent machine learning papers are in part
just demonstrating really impressive feats of engineering with their training
pipelines.

So far I've created the simplified environment (it needs more documenting) and
a smaller scale 2 x 6 board that uses a reduced piece set styled after
[this version from S. Melax](https://melax.github.io/tetris/tetris.html). When
I threw the [stable-baselines3](https://github.com/DLR-RM/stable-baselines3)
implementation of PPO at the smaller board environment I started to see
some promising signs of learning pretty quickly! Hopefully that indicates PPO
will be a promising application on the standard size board too.

# Reading List

- [Leaving A Legacy](https://littlegreenviper.com/miscellany/leaving-a-legacy/)
- [Remote working has been life-changing for disabled people, don’t take it
  away
  now](https://www.theguardian.com/commentisfree/2021/jun/02/remote-working-disabled-people-back-to-normal-disability-inclusion)
- [Do Wide and Deep Networks Learn the Same
  Things?](https://ai.googleblog.com/2021/05/do-wide-and-deep-networks-learn-same.html)
- [An Unbelievable
  Demo](https://brendangregg.com/blog/2021-06-04/an-unbelievable-demo.html)
- [How Replit used legal threats to kill my open-source
  project](https://intuitiveexplanations.com/tech/replit/)
- [The Secret IRS Files: Trove of Never-Before-Seen Records Reveal How the
  Wealthiest Avoid Income
  Tax](https://www.propublica.org/article/the-secret-irs-files-trove-of-never-before-seen-records-reveal-how-the-wealthiest-avoid-income-tax)
- [Engineering a chess match against my
  brother](https://blog.mbrt.dev/posts/chess-eng/)
- [Reward is
  enough](https://doi-org.ezproxy1.bath.ac.uk/10.1016/j.artint.2021.103535)
- [Don't Feed the Though Leaders (or ignore confident
  forecasters)](https://earthly.dev/blog/thought-leaders/)
- [On Audre Lorde's "The Master's
  Tools..."](https://www.countbayesie.com/blog/2020/6/5/on-audre-lordes-the-masters-tools)
