---
layout: post
title: "Rust is Safe for X"
date: 2025-01-10 10:55:00 -0700
categories: technical
tags: software-engineering rust type-safety 
---

I love [this article from lwn](https://lwn.net/Articles/995814/) and this conclusion especially: 
> this ability to take a property that the language does not know about and "teach" it to Rust, so that now it is enforced at compile time, is why he likes to call Rust an "X-safe" language. It's not just memory-safe or thread-safe, but X-safe for any X that one takes the time to implement in the type system.

<!--more-->

Rust is a language where you can use the type system to enforce safety guarantees at compile time. This isn't exclusive to Rust, it's a feature of any language with a strong type system. I think the ergonomics of Rust are particularly well suited to it, definitely over other systems languages.

I find myself coming back to this when we have implementation decisions. For example, if you are working on a service that has to handle encryption keys, you can use the type system to craft APIs and structs that simplify their handling. You can use a struct to ensure that your keys are never logged accidentally, by creating custom `Display` and `Debug` implementations that censor the plaintext. If you have multiple different kinds of encryption keys, you can craft APIs that require a key of type `Key<ComponentA>`, so you can't accidentally pass in the key for `ComponentB`. There are all sorts of nice things you can do here, and it's important to take advantage of them! 

I think a good rule of thumb is when you find someone saying "as long as...". As long as we use it in this way... As long as we pass it in the same way we receive it... That just means we know how we should use it, so we should encode that in the type system! People forget, people make mistakes. Lets make it easy on ourselves by making it _harder_ to make mistakes than to just use the API as intended. 