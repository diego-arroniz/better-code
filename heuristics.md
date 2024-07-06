# Heuristics

#### Inappropriate Information

It is inappropriate for a comment to hold information better held in a different kind of system such as your source code control system, your issue tracking system, or any other record-keeping system. Change histories, for example, just clutter up source files with volumes of historical and uninteresting text. In general, meta-data such as authors, last-modified-date, SPR number, and so on should not appear in comments. Comments should be reserved for technical notes about the code and design.

#### Obsolete Comment

A comment that has gotten old, irrelevant, and incorrect is obsolete. Comments get old quickly. It is best not to write a comment that will become obsolete. If you find an obsolete comment, it is best to update it or get rid of it as quickly as possible. Obsolete comments tend to migrate away from the code they once described. They become floating islands of irrelevance and misdirection in the code.

#### Redundant Comment

A comment is redundant if it describes something that adequately describes itself. For example:

```cpp
i++; // increment i
```

#### &#x20;Poorly Written Comment

A comment worth writing is worth writing well. If you are going to write a comment, take the time to make sure it is the best comment you can write. Choose your words carefully. Use correct grammar and punctuation. Don't ramble. Don't state the obvious. Be brief.

#### Commented-Out Code

It's not uncommon to see stretches of code that are commented out. Who knows how old it is? Who knows whether or not it's meaningful? Yet no one will delete it because everyone assumes someone else needs it or has plans for it.

That code sits there and rots, getting less and less relevant with every passing day. It calls functions that no longer exist. It uses variables whose names have changed. It follows conventions that are long obsolete. It pollutes the modules that contain it and distracts the people who try to read it. Commented-out code is an abomination.

When you see commented-out code, delete it! Don't worry, the source code control system still remembers it. If anyone really needs it, he or she can go back and check out a previous version. Don't suffer commented-out code to survive.

### Environment

#### Build Requires More Than One Step

Building a project should be a single trivial operation. You should not have to check many little pieces out from source code control. You should not need a sequence of arcane commands or context-dependent scripts to build the individual elements. You should not have to search near and far for all the various little extra JARs, XML files, and other artifacts that the system requires. You should be able to check out the system with one simple command and then issue one other simple command to build it.

#### Tests Require More Than One Step

You should be able to run all the unit tests with just one command. In the best case, you can run all the tests by clicking on one button in your IDE. In the worst case, you should be able to issue a single simple command in a shell. Being able to run all the tests is so fundamental and so important that it should be quick, easy, and obvious to do.

### Functions

#### Too Many Arguments

Functions should have a small number of arguments. No argument is best, followed by one, two, and three. More than three is very questionable and should be avoided with prejudice.

Arguments are even harder from a testing point of view. Imagine the difficulty of writing all the test cases to ensure that all the various combinations of arguments work properly. If there are no arguments, this is trivial. If there's one argument, it's not too hard. With two arguments the problem gets a bit more challenging. With more than two arguments, testing every combination of appropriate values can be daunting.

#### Flag Arguments

Flag arguments are ugly. Passing a Boolean into a function is terrible practice. It immediately complicates the signature of the method, loudly proclaiming that this function does more than one thing. It does one thing if the flag is true and another if the flag is false!

#### Dead Function

Methods that are never called should be discarded. Keeping dead code around is wasteful. Don't be afraid to delete the function. Remember, your source code control system still remembers it.

### General

#### Incorrect Behavior at the Boundaries

It seems obvious to say that code should behave correctly. The problem is that we seldom realize just how complicated correct behavior is. Developers often write functions that they think will work, and then trust their intuition rather than making the effort to prove that their code works in all the corner and boundary cases. There is no replacement for due diligence. Every boundary condition, every corner case, every quirk and exception represent something that can confound an elegant and intuitive algorithm. Don't rely on your intuition. Look for every boundary condition and write a test for it.

#### Duplication

This is one of the most important rules in this book, and you should take it very seriously. Virtually every author who writes about software design mentions this rule. Dave Thomas and Andy Hunt called it the DRY principle (Don't Repeat Yourself). Kent Beck made it one of the core principles of Extreme Programming and called it: "Once, and only once."

Every time you see duplication in the code, it represents a missed opportunity for abstraction.

#### Inconsistency

If you do something a certain way, do all similar things in the same way. This goes back to the principle of least surprise. Be careful with the conventions you choose, and once chosen, be careful to continue to follow them.

If within a particular function you use a variable named `response` to hold an `HttpResponse`, then use the same variable name consistently in the other functions that use `HttpResponse` objects. If you name a method `processVerificationRequest`, then use a similar name, such as `processDeletionRequest`, for the methods that process other kinds of requests. Simple consistency like this, when reliably applied, can make code much easier to read and modify.

#### Clutter

What use is a default constructor with no implementation? All it serves to do is clutter up the code with meaningless artifacts. Variables that aren't used, functions that are never called, comments that add no information, and so forth. All these things clutter and should be removed. Keep your source files clean, well-organized, and free of clutter.

#### Function Names Should Say What They Do

Look at this code:

`Date newDate = date.add(5);`

Would you expect this to add five days to the date? Or is it weeks, or hours? Is the date instance changed or does the function just return a new Date without changing the old one?

You can't tell from the call what the function does. If the function adds five days to the date and changes the date, then it should be called `addDaysTo` or `increaseByDays`. If, on the other hand, the function returns a new date that is five days later but does not change the date instance, it should be called `daysLater` or `daysSince`.

If you have to look at the implementation (or documentation) of the function to know what it does, then you should work to find a better name or rearrange the functionality so that it can be placed in functions with better names.

#### Understand the Algorithm

Lots of very funny code is written because people don't take the time to understand the algorithm. They get something to work by plugging in enough if statements and flags, without really stopping to consider what is really going on.

Programming is often an exploration. You think you know the right algorithm for something, but then you wind up fiddling with it, prodding and poking at it, until you get it to "work." How do you know it "works"? Because it passes the test cases you can think of. There is nothing wrong with this approach. Indeed, often it is the only way to get a function to do what you think it should. However, it is not sufficient to leave the quotation marks around the word "work."

Before you consider yourself to be done with a function, make sure you understand how it works. It is not good enough that it passes all the tests. You must know that the solution is correct.

Often the best way to gain this knowledge and understanding is to refactor the function into something that is so clean and expressive that it is obvious how it works.

#### Follow Standard Conventions

Every team should follow a coding standard based on common industry norms. This coding standard should specify things like where to declare instance variables; how to name classes, methods, and variables; where to put braces; and so on. The team should not need a document to describe these conventions because their code provides examples.

#### Avoid Negative Conditionals

Negatives are just a bit harder to understand than positives. So, when possible, conditionals should be expressed as positives. For example:

`if (buffer.shouldCompact())`

is preferable to

`if (!buffer.shouldNotCompact())`

### Names

#### Choose Descriptive Names

Don’t be too quick to choose a name. Make sure the name is descriptive. Remember that meanings tend to drift as software evolves, so frequently reevaluate the appropriateness of the names you choose. This is not just a “feel-good” recommendation. Names in software are 90 percent of what make software readable. You need to take the time to choose them wisely and keep them relevant. Names are too important to treat carelessly. Consider the code below. What does it do? If I show you the code with well-chosen names, it will make perfect sense to you, but like this it’s just a hodge-podge of symbols and magic numbers.

```java
public int x() {  
  int q = 0;  
  int z = 0;  
  for (int kk = 0; kk < 10; kk++) {  
    if (l[z] == 10) {  
      q += 10 + (l[z + 1] + l[z + 2]);  
      z += 1;  
    } else if (l[z] + l[z + 1] == 10) { 
      q += 10 + l[z + 2];  
      z += 2;  
    } else {  
      q += l[z] + l[z + 1];  
      z += 2;  
    }  
  }  
  return q; 
}
```

Here is the code the way it should be written. This snippet is actually less complete than the one above. Yet you can infer immediately what it is trying to do, and you could very likely write the missing functions based on that inferred meaning. The magic numbers are no longer magic, and the structure of the algorithm is compellingly descriptive.

```java
public int score() {  
  int score = 0;  
  int frame = 0; 
  for (int frameNumber = 0; frameNumber < 10; frameNumber++) {  
    if (isStrike(frame)) {  
      score += 10 + nextTwoBallsForStrike(frame);  
      frame += 1;  
    } else if (isSpare(frame)) {  
      score += 10 + nextBallForSpare(frame);  
      frame += 2;  
    } else {  
      score += twoBallsInFrame(frame);  
      frame += 2;  
    }  
  }  
  return score;  
}
```

The power of carefully chosen names is that they overload the structure of the code with description. That overloading sets the readers’ expectations about what the other functions in the module do. You can infer the implementation of `isStrike()` by looking at the code above. When you read the `isStrike` method, it will be “pretty much what you expected.”

```java
private boolean isStrike(int frame) {  
  return rolls[frame] == 10; 
}
```

#### Unambiguous Names

Choose names that make the workings of a function or variable unambiguous. Consider this example:

```java
private String doRename() throws Exception {  
  if(refactorReferences)  
    renameReferences();  
  renamePage();
  pathToRename.removeNameFromEnd();  
  pathToRename.addNameToEnd(newName); 
  return PathParser.render(pathToRename);  
}
```

The name of this function does not say what the function does except in broad and vague terms. This is emphasized by the fact that there is a function named `renamePage` inside the function named `doRename`! What do the names tell you about the difference between the two functions? Nothing. A better name for that function is `renamePageAndOptionallyAllReferences`. This may seem long, and it is, but it’s only called from one place in the module, so its explanatory value outweighs the length.

#### Use Long Names for Long Scopes

The length of a name should be related to the length of the scope. You can use very short variable names for tiny scopes, but for big scopes you should use longer names. Variable names like `i` and `j` are just fine if their scope is five lines long. Consider this snippet from the old standard “Bowling Game”:

```java
private void rollMany(int n, int pins) {  
  for (int i = 0; i < n; i++) 
    g.roll(pins); 
}
```

This is perfectly clear and would be obfuscated if the variable `i` were replaced with something annoying like `rollCount`. On the other hand, variables and functions with short names lose their meaning over long distances. So the longer the scope of the name, the longer and more precise the name should be.

#### Names Should Describe Side-Effects

Names should describe everything that a function, variable, or class is or does. Don’t hide side effects with a name. Don’t use a simple verb to describe a function that does more than just that simple action. For example, consider this code:

```java
public ObjectOutputStream getOos() throws IOException {  
  if (m_oos == null) {  
    m_oos = new ObjectOutputStream(m_socket.getOutputStream());  
  }  
  return m_oos;  
}
```

This function does a bit more than get an “oos”; it creates the “oos” if it hasn’t been created already. Thus, a better name might be `createOrReturnOos`.

### Tests

#### Insufficient Tests

How many tests should be in a test suite? Unfortunately, the metric many programmers use is “That seems like enough.” A test suite should test everything that could possibly break. The tests are insufficient so long as there are conditions that have not been explored by the tests or calculations that have not been validated.

#### Don’t Skip Trivial Tests

They are easy to write and their documentary value is higher than the cost to produce them.

#### Tests Should Be Fast

A slow test is a test that won’t get run. When things get tight, it’s the slow tests that will be dropped from the suite. So do what you must to keep your tests fast.
