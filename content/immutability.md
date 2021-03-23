+++
title = "Immutability - what's it all about"
description = "Yet another article about immutability"
date = 2021-03-16
draft = false
+++

Recently I've been interviewing more than usual and I've been surprised how often immutability seems to be poorly understood or considered irrelevant. Most of the time when I ask about immutability, the answer I get is - _It makes dealing with concurrency easier._ 

It reminds me of how often "it's easy to implement undo" was brought into discussion when immutability started reaching frontend world. And yes, immutability makes concurrency easier, it makes it easy to implement undo, but that's missing the big picture. 

Immutability is mainly identified with functional programming, but it's benefits have been well known to OO community too. [Effective Java](https://bookshop.org/books/effective-java-9780134685991/9780134685991), with first edition released 2001, has a chapter titled "Minimize mutability" which details why immutability is important and ends with following advice "Classes should be immutable unless there's a very good reason to make them mutable". Yet immutability seems quite foreign to OO programmers. 

Immutable object is an object which can't be modified after it's initialized. If we step aside from OO world, it's memory which can't be modified after it has been initialized. What this means is that objects state is decided on during creation time and only creation time. If you want to mutate the object, you have to create a new one. 

#### So what's the big deal? 

Simply put, immutability makes it easier to think about your code and harder to write bad code. It is achieved through various mechanisms that I'll try to list them here.

**Invariant** is a set of properties which remain true during objects lifecycle. In practice, it's a contract between class creator and class users which tells users how the class behaves. In OO, encapsulation is the way of maintaining class invariant - state isn't accessible from the outside and object itself maintains it after every method call. Keeping the invariant this way can get tricky. And even then, often there are some weird edge state transitions which break the invariant. 

With immutability, invariant is established the moment object is created and can never be violated. This also gives us what Bloch calls **failure atomicity** for free. If object is instantiated correctly, it will always be in valid state. It's impossible for object to be in temporary inconsistent state.

Closely related is **reduced state space**. Mental process used for reasoning about the code often resolves around mental simulation of code behavior. As number of states grows, number of possible scenarios grows exponentially and effectiveness of our reasoning plummets. Immutable objects can be in only one state, the one they were created at. The reduced state space makes it possible for us to reason about the code.

This also translates to **easier testing and debugging**. If it's easier to reason about the code, it's easier to test and debug. Captain Obvious quote right there. And it doesn't stop there. How many times did you have to get the object in some specific state to reproduce the bug? With immutability this isn't a problem, if you can't create the object in certain state, it can't get into that state. Simple as that. 

**Sharing** is another benefit. It obviously includes previously mentioned concurrency, but it's also more than that. You can share the internals of immutable object or data structure. In the end, that's how efficient persistent data structures work. By knowing underlying structure can't change, you can just reuse the internal structure. How many times have you defensively copied an object? With immutable object there's no need. And then there's concurrency. Immutable objects lend itself to concurrency because one thread can't change it underneath other one. Immutable objects make dealing with concurrency as easy as possible.

**Imperative programming is harder** when using immutable data. And yes, this is a good thing, Imperative programming uses statements to change program's state. And by now we should be aware that state = bad. 

Immutable data is **easier to use as building block** of different objects. The extreme case of this is using it in maps or sets. What does it mean if an object inside of HashSet mutates? How should the set behave? It also makes it more natural to compose objects. Inheritance comes with it's own set of problems and composition is generally the way to go. 

#### If immutability is so awesome, why isn't it everywhere?

Turns out there was a very good reason for that - performance. Historically, memory was expensive. NASA has sent man to the moon with memory that can be found in car keys today. When every byte matters, immutability just isn't feasible. Performance is also a reason why mutable languages, just like low level languages are still needed. 

The good news is memory got cheap. Most of our systems aren't resource constrained anymore and today immutability is feasible almost everywhere.


#### Immutability changes everything

I've shamelessly stolen the subtitle here from Pat Helland's paper[^first], but I find it appropriate. It seems counterintuitive that adding constraints makes programming easier. It's a trade off between how hard it is to write the code and how hard it is to read, test and think about it. In the end, we're writing it only once, but reading it multiple times. I'll finish off repeating the quote from Effective Java:

> Classes should be immutable unless there's a very good reason to make them mutable. 


#### References
1. [Effective Java](https://bookshop.org/books/effective-java-9780134685991/9780134685991)
1. [Out of the Tar Pit](http://curtclifton.net/papers/MoseleyMarks06a.pdf)
1. [The Value of Values](https://www.infoq.com/presentations/Value-Values/)
1. [Refactoring to Immutability](https://vimeo.com/234107745)
1. [The Joy of Clojure](https://bookshop.org/books/the-joy-of-clojure/9781617291418)

#### Footnotes

[^first]:  Pat Helland's [paper](http://cidrdb.org/cidr2015/Papers/CIDR15_Paper16.pdf) talks about immutability in distributed context though, think HDFS as an example, while this article is more about lower level.