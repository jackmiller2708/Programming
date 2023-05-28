So this is the first real section, and we're kicking it off with something really important. Something big. It's called Big O notation. And when I say big, I don't mean that it's long or difficult. It's big in significance. It's something that we basically are going to refer back to what we talk about in this section later on in other sections. So before I even explain what it is, I have a quick warning. 
> [!warning]
> There's a bit of math in this section

And I'm warning you not to scare you away, but actually to encourage you to push through it. If you do struggle with math or if you're someone who hasn't heard the word logarithm ever, or in 10 or 20 years; that's going to come up in this section at the end. But don't panic, because what we're going to do here in this section is establish a framework for talking about code in the rest of the roadmap. And that does involve some math up front, but it doesn't mean that the rest of the roadmap is going to be, some of it will be mathy, definitely. But this is not indicative of what the rest of the roadmap will look like. So just **PUSH THROUGH IT!!**. I mean if you like math, great. If you have some problems with this section, just remember that the entire roadmap isn't like this and we're just getting it out of the way. Because, like I said, it has to come first. _I don't really have a choice_. 

Okay, sorry if I scared anybody there. 

## Objectives
Let's talk about the objectives for this section. So we're going to start by just talking about the need for something like Big O notation:
- I haven't even mentioned what it is, so we're going to get to that. 
- Then we're going to describe it. Why we care about it?
- We're going to learn to simplify.
- Big O expressions will define **time and space**, 
- will evaluate time and space complexity of different algorithms using big O notation. 
- And then we'll describe what a logarithm is - a bit of math at the end there. 

So I know it's a lot, but we're going to start with this first  point, motivate the need for something like Big O notation.

## Motivation
So... what is the idea here? 

Well, this roadmap is about algorithms, solving challenges, computer science and data structures. But for every topic in this roadmap, there's 10-20 different implementations or solutions that could work, probably way more. 

How do we know what's best? So let's scale it down a bit just to a single problem. Let's say that there are two valid solutions to a problem. They both work and they're different, not just in names or variable names or something, but totally different in approaches. One uses a loop, the other uses, I don't know, a list or a string or something to accomplish the same task. How do we know which one is best? 

That's really what Big O is about. It's a system. It's a way of generalizing code and talking about it and comparing code and its performance to other pieces of code. So here's a more concrete example: 
>Write a function that accepts a string input and returns a reversed copy. 

If I asked you to do this, which maybe some enterprising students will do this and come up with some creative solutions off the top of my head, I can come up with three-ish solutions, different approaches, and I'm sure there are way more out there. I actually found this post on [Stack Overflow that has ten different implementations in JavaScript and they're all different](https://stackoverflow.com/a/26610963). 

Like it said, it's not just a different variable name, it's not just switching a for loop for a while loop. There are different approaches. How do we know if all of these work? Here's one using a for loop and an array. 
```javascript
function reverse(s) {
  var o = [];
  for (var i = s.length - 1, j = 0; i >= 0; i--, j++)
    o[j] = s[i];
  return o.join('');
}
```
Here's one that uses no loops and no arrays. 
```javascript
function reverse(s) {
  return (s === '') ? '' : reverse(s.substr(1)) + s.charAt(0);
}
```
It's all actually - I guess there is an array in there at one point - built in methods. 

How do we know which one is best? Well, we'll get there. But wouldn't it be nice if there was sort of a system for classifying code or for comparing it, which I've already spoiled it and said, that's a big O, sort of. 

## Understanding

Think of it sort of like if we're talking about earthquakes. This was a seismology 101 class. Very early on, I would start off by talking about the Richter scale because then that allows us to talk about earthquakes and compare them to one another so that instead of just saying _"Oh, there's a big earthquake and then a bigger one over there"_, we can say _"there was a 7.5 and then a 9.2 over there"_. And that puts things into context. That's kind of not a great analogy, but the idea is that we can assign labels, generalized labels, to our code. So instead of saying something like great or awful for our code, we can have a numeric representation of the performance of code. So that's what Big O is going to give us rather than colors and text like, great. It's going to look a little bit different. It might look a little mathy, but it's actually pretty straightforward once you get past the first hurdle of it looking very foreign and weird. 

So one last point I want to make. Some of you might be wondering if I asked you to write a function that reverses string and you get it to work, doesn't it only matter that you get it to work? Like, why does it matter what's best? The solution you come up with is the best. And in some ways I think that, depending on your project in the context that's true. 

The best solution is the one that you can get to work. But when we're talking about things like interviewing, technical interview, code challenges or working at a large company where you're working with a huge data set. Let's say hundreds of millions of pieces of data where one algorithm implementation could save an hour every time it runs compared to another implementation. Performance matters at that point, and there is an actual best algorithm or best solution. So it's important to have a precise vocabulary to talk about how our code performs. So even if you're content with your solution to something, it's helpful to be able to understand how it compares, how it performs compared to others. 

It's also good for discussing trade offs between different approaches because often it's not as cut and dry as I made it seem. It's not that one solution is always great and the other one is always terrible. Sometimes one solution might be great at handling really large data sets, pieces of data. Another one might always be very consistent and the time that it takes, but it might take more time. Up front, there's trade offs. So it's not always just this is the best. 

Also, if you're trying to debug your code, it helps to understand things that are slowing it down, not just looking for errors, but let's say that your code is working. But for some reason it's taking a lot longer than you expect or your computer is lagging and freaking out in the browser. 

When you execute some function, it helps if you understand some of the things we're going to talk about in this section. In Big O notation, you can actually pinpoint where some problems might arise. So it helps us identify inefficient points. And then finally you should care because it comes up in interviews a lot. A lot of times an interviewer will say something like, Tell me the big O of this algorithm, or if this function that you've written or Here's three functions, what's the big O? That will make sense in a bit. But it's important just to know for interviews, I said it's less important because hopefully you're learning it to actually understand things and to help you understand your code better and talk about your code better, rather than just directly trying to master it for an interview. But interviews are important, so no judgment there either.

## Timing Our Code

All right. So let's take a look at a more concrete example. Let's compare two solutions to the same problem. 

So here's our problem:
>Suppose you want to write a function that calculates the sum of all numbers from one up to and including some number `n`. 

So if we plug `3` in, we should get `1 + 2 + 3`, which is `6`. The most common or the easiest to come up with solution:
```JS
function addUpTo(n) {
  let total = 0;
  for (let i = 0; i < n; i++) {
  	total += i;
  }
  return total;
}
```
This is the one that comes to my mind first. It is to basically create a total variable accumulator and loop through all those numbers and add them in one at a time, starting at one all the way up until `n`. So that's what I've done here. We have a for loop. 
```JS
// ...
for (let i = 0; i < n; i++) {
  total += i;
}
// ...
```
Total variable starts at zero
```JS
// ...
let total = 0;
// ...
```
and at the end we return total. 
```JS
// ...
return total;
```
We start the loop at one, we go up until `n` each time through total plus equals. 

Next, there's a second solution. There's more than these two, but these are two that I'm going to use because they illustrate my point. 
```JS
function addUpTo(n) {
  return n * (n + 1) / 2;
}
```
This one is definitely less intuitive. As you can see, it's a lot shorter. It's a single line which doesn't necessarily make it better, but it's very different. There's no loop involved. What we're doing is more of a mathematical formula. We take `n` and we multiply it by `n` plus `1` divided by `2`. It gives us the same answer in the end. 

So we establish there are two working solutions, _which one is better?_ And of course, the first thing that we could ask is _what does "better" actually mean?_ Does it mean _the faster code in seconds or milliseconds?_ Does it mean _the code that's fastest when we're adding a small number versus a large number?_ Let's say we want to benchmark it out when we add up all the numbers between 0 and 1 billion, _is that a good test or is it about how much memory is used?_ _Is it the number of variables that are created, the data that is stored each time that that function is called? Or what about something like readability, legibility?_ _How important is that? Is that better? Or brevity?_ That's not on here. But a lot of people care about that. They like to minimize the the length, the number of characters used in their programming. Not my style personally, but definitely valid. All of these are valid concerns and it really comes down to the situation. But I think most people would agree that the first two, specially for now, we're going to focus on speed. We'll come back to memory usage in a bit. But these two often can be more important than something like readability, and unfortunately they often come at the expense of readability. And that's sort of the balancing act of writing good code is writing efficient code that doesn't use up a ton of memory, but also is still readable and doesn't look like complete gibberish. So we're going to talk about basically all how all of these play together throughout the entire roadmap. It will be a recurring theme, but we're going to focus on evaluating speed, how long code takes to execute. 

How do we do that? Well, the simplest way would be to use something like built in timing functions, 
```JS
function addUpTo(n) {
  let total = 0;
  for (let i = 0; i < n; i++) {
  	total += i;
  }
  return total;
}

let t1 = performance.now();
addUpTo(1000000000);
let t2 = performance.now();
console.log(`Time Elapsed: ${(t2 - t1) / 1000} seconds`);
```
something like this where we have our first add up to. 
```JS
function addUpTo(n) {
  let total = 0;
  for (let i = 0; i < n; i++) {
  	total += i;
  }
  return total;
}

// ...
```
And then I use a function called or a method called performance now,
```JS
// ...

let t1 = performance.now();
// ...
```
which in the browser is just going to tell me the number of milliseconds since the document was created, basically since I opened the window. And then so I'm going to save that to a variable before I call `addUpTo`, then I'm going to call `addUpTo` with, 
```JS
// ...
addUpTo(1000000000);
// ...
```
what did I do? It's a **BILLION!!**. And then after that finishes, I'm going to check performance now again, 
```JS
// ...
let t2 = performance.now();
// ...
```
which should have incremented a bunch of milliseconds, most likely. So I have two numbers, then I just subtract them the first or the second time, minus the first time, and I divide it by 1000 because it's in milliseconds and I want to work in seconds, we don't have to do that last part,
```JS
// ...
console.log(`Time Elapsed: ${(t2 - t1) / 1000} seconds`);
```
and I print it out. So `addUpTo`, our same one, from before and we're calling it with 1 billion and we're going to print out how long elapsed. 
```console
Time Elapsed: 0.9968000001907349 seconds
```
Let's go over to the second solution. 
```JS
function addUpTo(n) {
  return n + (n + 1) / 2;
}

let t1 = performance.now();
addUpTo(1000000000);
let t2 = performance.now();
console.log(`Time Elapsed: ${(t2 - t1) / 1000} seconds`);
```
I'm doing the same thing. Taking performance out now at the beginning and performance out now at the end. So now if I run this, 
```console
Time Elapsed: 0 seconds
```
you can see we get a way smaller number, this is significantly shorter in duration with the same data as the other one, `0.9968000001907349 seconds` compared to basically `0 seconds`. 

So that seems like a good sign for this solution. It seems like it's much more efficient and that's great. But this process is not the most reliable of manually timing things like this before and after and comparing it to the other function. And it's not that easy for us to talk about. How would I actually write down? How would I give it a label of how efficient this one is compared to this one? Is it based off of the percentage of speed? Is it the "I subtract the number of seconds or milliseconds"?, it gets a little blurry. This brings us to _the problem with time_, which I'm reserving for my end of life memoir title: **The problem with time** - It's just a nice little sound, very deep. 

So the first is that different machines will record different times, so it's not reliable depending on the specifications of a machine and what's currently happening on that machine, what code is running the time and the results you can get will be different. That doesn't really mean that we'll get the opposite results where the first solution is suddenly faster than the second one. But it means that the margins could change. The actual measurements could be different and are almost guaranteed to be different times. It's not precise and that we can't rely on that. And second of all is that for fast algorithms, things that are happening on a really, really fast scale, speed measurements might not be precise enough. We have two or three or four algorithms and they're all super fast and they're doing something very quickly. There still is one that is going to be fastest or most efficient, but if our timing functions can't figure it out because they're the smallest interval of time that can be measured isn't good enough, then it doesn't really help us. 

So how do we walk through our code and actually talk in general terms about which code is better without having to go and time it? 
> [!info]
> I want to be clear. I'm not saying that timing your code is a bad idea. I do it all the time, but I'm more saying is that it would be cool if there was another way that didn't involve having to set up a new file and actually go through the process of timing our code. 

What if our code takes an hour? Something massive, and I'm comparing it to another version that takes 4 hours. I don't want to have to run a test to figure out which one is faster. We want to be able to assign a value to in general terms, talk about how code compares to other code without having to go through all of this. And that's where big O notation comes in.