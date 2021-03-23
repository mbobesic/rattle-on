+++
title = "Intro to unit tests"
description = "Article about what are unit tests, how they help you and how to avoid common pitfalls."
date = 2021-02-26
draft = false
+++

It seems like unit tests are the biggest problem every time an intern/junior developer joins the team. As a intro to world of unit tests I decided to write yet another article about unit tests.

## What are unit tests

Commonly for software engineering, there is plenty of definitions. Just google it and you will find more than enough. Rather than using the definition, I'll just point out important characteristics of unit tests:

* they test smallest unit of code
* unit is tested independently from other units
* fast to run
* written by developers

## What are unit tests good for

Well, not for catching bugs. At least not the first time you write the code. Unit tests are good for:

1. [Testing if your code sucks](#testing)
2. [Quick feedback loop](#qfl)
3. [Getting familiar with the code when you didn't write it (or it was you months ago)](#gfc)
4. [Catching bugs when you refactor (when changing implementation details, not behavior)](#cb)

### Testing if your code sucks {#testing}

If your unit tests are difficult to write, it usually means something is wrong with the code. And this is the biggest use case for unit tests.
Some possible causes are:
* The code is too coupled
* Single responsibility principle violations
* Using inheritance instead of composition
* Violations of open-closed principle

Now the bad news. Dijkstra said testing can prove existence of bugs, but never absence of them. Similarly, unit tests can prove your code sucks, but can't prove it doesn't.

### Quick feedback loop {#qfl}

Unit tests give us quick feedback loop to confirm or deny our expectations from the code. I have seen so many times people dropping jars on a server just to test couple of lines of code change. Doing so increases testing time from seconds to minutes.

### Getting familiar with the code {#gfc}

No matter how much we try, old code is rarely easy to read, even if it was written only couple of months ago. Best code practices are changing and reading code from 5 years or more can be exhausting. Unit tests are form of documentation which tells us how the code is supposed to work.

Quick feedback loop plays a role here too. If you are not sure about some part of the code, change it and see what fails. Learn about the code, do the test and confirm or refute your understanding.

### Catching bugs {#cb}

When first writing unit tests, they rarely find bugs. If your design is wrong, your unit tests will be wrong (_side note: fixing a bug isn't cheapest in development, but in design_). The type of bugs found in first iteration are usually simple bugs caused by accidentally autocompleting something wrong or something trivial like that. That's not to say they can't be extremely painful to find.

But they do catch bugs when changing implementation without changing behavior. And at least make refactoring a bit less risky.

## Writing unit tests is easy...

Answering following 3 questions is all that is needed:

1. What behavior are you validating?
2. What are the inputs?
3. What is expected output/behavior?

##  ... writing testable code is hard

Methods ordered by "how easy to test" are:

1. Pure functions
2. Methods without side effects
3. Methods that do only one thing
4. Other methods

Pure functions are functions whose output depends only on function/method parameters and produces no side effects. Inputs to unit tests are function parameters and output is return value.

As methods without side effects I consider methods that don't change state but depend on it in it's computation. Inputs are coming from object state and possibly function parameters. Output is return value.

Methods that do only one thing are not pure functions or methods without side effects are next. Their inputs are object state or possibly function parameters (can be either or both). In this case we don't have output, but expected behavior. Expected behavior is either change in state of the object xor invoking method on another object.

And as far as all others are concerned, please no. Everything else means it returns a value and changes state. Change in state can be in current object and delegated further on a different object. In any case, it means we are both changing the state and returning a value and by doing so violating single responsibility principle.

Prefer pure functions and immutable objects. They will make your life easier.

## Testing code smells

There is great [article](http://misko.hevery.com/attachments/Guide-Writing%20Testable%20Code.pdf) by Misko Hevery about this topic so I won't go into it, I'll just list the smells I found most often:

* Constructor does real work
* Mixing object creation with business logic (not using DI)
* Digging into collaborators
* Global state
* Class does too much
* Conditional Slalom
* Pass around giant context object
* Side effects
* Deep inheritance
* Static methods which are not pure functions

## Unit test smells
In [Pragmatic Unit Testing in Java](https://pragprog.com/book/utj/pragmatic-unit-testing-in-java-with-junit) Hunt and Thomas say:
_"If the answer is not obvious, or it looks like the test would be ugly or hard to write, then take that as a warning signal. Your design probably needs to be modified; change things around until the code is easy to test, and your design will end up being far better for the effort."_

Some of the unit tests smells which suggest code probably should be refactored are:

### Unit testing private methods

Unit tests should test behavior, not implementation details. Quick sort and merge sort should have identical unit tests. If you do fell the need to unit test private methods, it usually means that class is too big and should be refactored.
Unit testing private methods also has bigger effect on technical dept as you lose static typing and any help your IDE might provide when refactoring.

### Setting and Accessing internal object state

State should have initial value. Initial values should be set in constructor. We can easily pass the expected value to the constructor. If the value isn't available at the construction time, it should be a method parameter.

### Using library like PowerMock

[Power mock](https://github.com/powermock/powermock) library says: _Please note that PowerMock is mainly intended for people with expert knowledge in unit testing. Putting it in the hands of junior developers may cause more harm than good._

Sometimes it's needed. Most of the time, it's not. If you are not sure if you need PowerMock, you probably don't.

### Testing multiple behaviors in one test

Testing multiple behaviors in one test suggests Single Responsibility Principle violations. If not in the method being tested, then in the test itself.

### Unit tests are not independent

If we want to test two methods, that's are functional tests. Otherwise unit tests should be independent. Difficulty writing independent tests can mean that methods aren't independent either.

### Unnecessary preconditions

When coming to code for the first time, you rely on reading the code and unit tests. Unnecessary preconditions are lying and make understanding old code even more difficult.

### Unnecessary assertions

Similar to unnecessary preconditions, but with one additional issue. Developer will think unnecessary assertions were part of original requirements. There are plenty of requirements even without us artificially adding new ones.

### Common setup(@Before in java) code not used by all methods

It actually means there are unnecessary preconditions, probably in multiple tests. Additionally, it can also suggest class is too big.

### Forgetting about clean code in tests

Unit tests will be read and maintained, just as normal code will be read, with the costs of maintaining them. Technical dept applies to unit tests too.

## Conclusion

Unit tests are not a silver bullet, but they are helpful tool which can help you write better code and iterate faster. On other hand, maintaining unit tests on untestable code can make your life extremely painful and make you move even slower.
