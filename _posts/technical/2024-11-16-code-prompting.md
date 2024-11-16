---
layout: post
title: "Prompting Experiments"
date: 2024-11-16 10:00:00 -0000
categories: technical
tags: software-engineering gen-ai claude-3.5 anthropic
---

I'm on vacation, so I'm getting some time to do things that interest me in between time spent with family and recharging. As part of that, I wanted to write a blog on [turmoil](https://github.com/tokio-rs/turmoil) and how to use it for testing, and I've ended up yak-shaving my way into making a preprocessor for mdBook to compile examples that use external dependencies. I say making instead of writing, because I prompted my way to a solution. 

<!--more-->

This took me all of 8:00am to 9:30am today to get a working solution. This feels very much in a similar vein to [Marc Brooker's](https://www.linkedin.com/posts/marc-brooker-b431772b_one-thing-ive-enjoyed-in-the-run-up-to-re-activity-7255614212155006976-k47m?utm_source=share&utm_medium=member_desktop) experience with gen AI coding tools. It's great for small, greenfield tasks where you want a solution, but don't have the time to dive into all of the weeds yourself. 

Here I was using Claude 3.5 Sonnet to iterate. It's incredibly impressive how it feels like having a junior engineer to execute your ideas that responds in 2-5 seconds instead of 5+ hours. I've added the chatbot log to the repo to keep a record of what it was like to actually iterate and reach the solution. There's a few things I need to do before I can hopefully share. 

The code itself isn't particularly long, and it's mostly glue that's supported by other incredible open source projects (mdBook and the whole Rust ecosystem). However, I still find it super impressive that this is where we are at. It feels like a step change in tooling. I'm having more and more of these moments when it comes to reaching to gen AI to help me fill a gap in my available tools. 

Long term, would I blindly use this crate? No. I think I would go through the code with a line by line review before publishing, add some TODOs and make notes of the sketchier parts that are likely to bite you. But to get a solution off the ground in no time at all, it's awesome.

Now I can get back to the blog writing I actually meant to do.