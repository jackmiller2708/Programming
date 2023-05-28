## Objects performance

So let's begin by talking about [[Plain Objects|objects]], talking about them through the lens of [[Big O Notation|Big O and performance]]. Hopefully you're familiar with them. 

Objects work well when you don't need order, of course. And also when you want fast access and insertion and removal. No order, but almost everything else is very quick. And when we say quick, I'm talking about constant time for __insertion__, __removal__ and __accessing__ data. That's the fastest we can go - _✨constant time✨_. We'll come back to searching in a moment. We'll later down the road have a section called [[Hash Tables|hash maps]] where we actually learn a [[Data Structure Intro|data structure]] that explains how objects work behind the scenes, how things are actually stored. So, here's an object:
```JS
let instructor = {
  firstName: 'Kelly',
  isInstructor: true,
  favoriteNumber: [1, 2, 3, 4],
}
```
What happens when when we say `instructor` should have `firstName` set to `'Kelly'`? What does JavaScript actually do? A computer can't necessarily just access a place in memory called `firstName`, so there's some additional steps involved along the way. There's something called __"hashing"__. We'll talk about it later down the road, but all that you need to know is that JavaScript is able to add something into an object, a new piece of information, in constant time. It's also able to retrieve something in constant time, and you could also update something in constant time, which is really the same as retrieving it, you're just changing it. Same with removal. 

So it's quick, it's fast, for all the basic operations. There is no order, so there's no beginning of the object, there's no end. It doesn't matter where you insert because there is __"nowhere"__. That's a bad way of putting it. But you can't insert at the beginning or in the middle or the end of the object. There's no repercussions, you just add in using a _key_. 

Insertion, removal and access are all constant time. Searching, however, is O(n) - it's linear time. And when we say searching, it doesn't mean looking for a key, For example `firstName`, because as we've already seen, accessing information with a key is constant time. What I'm talking about is checking to see if a given piece of information is in a value somewhere. If it's on the right side of the colon, we have no easy way of doing that. We would potentially have to check every single item, every property. If we wanted to know, is `true` stored in our object somewhere, we'd have to check `firstName`, what's your value? And then we look at it. It's `'Kelly'`. All right, that's not it. `isInstructor` What's your value? `true`. So there is `true` in here, but potentially as the number of properties in there grows, as n - as in O(n) - grows, so does the amount of time it takes to do that. 

So now let's go on to some of the methods that objects come with things like [keys](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys), [values](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/values) and [entries](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/entries). Those three are all O(n). let's take a look at `keys`, 
```JS
Object.keys(instructor);
```
so it's `Object.keys()` and then we pass in the `instructor` object. We get this array with the keys. 
```JS
['firstName', 'isInstructor', 'favoriteNumbers'];
```
This is O(n) time because as the number of items in there grows, we're going to have to visit every single thing once and add it to this array. Same thing with `values`. Hopefully that makes sense. 

If we have 100 elements/properties in our object, there's 100 operations we need to do. There's usually more, but it runs roughly in line with O(n). It might be O(2n), it might be O(50n), but that still simplifies to O(n) and then that also is the same for `entries`, right? Technically, `entries` is a little more work, potentially having to compile the key and the value, but it all just simplifies to O(n) at the end of the day. 

Lastly, we've got [hasOwnProperty](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty) and it is a little different. We pass in a property like `firstName` and it just tells us it has `firstName` or not in constant time, and hopefully that makes sense why it's constant time.

So in summation, objects are really quick for pretty much everything. However, there's no order and as we'll see coming up with arrays, arrays can be pretty fast for a lot of things, but the order also can slow them down depending on what we're doing. Objects are basic. They work very well in a lot of situations. All operations - inserting, accessing, updating, removing - in constant time; Searching is pretty rare, but it is O(n) it grows as n grows, it's linear, and then the methods like `keys`, `values` and `entries` where we're creating an array based off of the data of object. As the object grows, so does the number of operations, the amount of time it takes to compile those and are often O(n). Next, array is a little more interesting because there's some variation, there's some nuance to it. 
## Array Performance
Let's talk about arrays through the lens of Big O performance and how do they compare to objects. The big selling point of arrays, of course, is that they are __ordered__. There is an intrinsic ordering to the data, unlike an object, where things just float around in a gelatinous mass. And that's often very useful if we need order, but it can come at a cost for some of the operations. 

Anyway, here are two different arrays. 
```JS
let names = ["Michael", "Melissa", "Andrea"];
let values = [true, {}, [], 2, "awesome"];
```
Of course you can store whatever you want in there, different types of data; And each element has an index, a numeric value that corresponds to it. So the first element is the zeroth item, the second is first, the third is second. These are called _"general arrays"_ since they're arrays and are generic. You use them when you need order. If you don't need order, then you probably don't want to use an array. If you're just trying to store random data together, you could still use an array, but if you're really trying to optimize for performance, there are other options. And even if you do need order, we're going to see some other structures coming up, like a [[Singly Linked Lists|singly linked]] list and a [[Doubly Linked Lists|doubly linked list]] that still encode order. Arrays are not the only ordered data structure on Earth, they're just the only one that we get for free in JavaScript, but often that can come at a cost depending on what you're trying to do, especially around insertion and removal, it can complicate things. 

Accessing data in an array is always very quick, it's is O(1), just the exact same as we talked about with an object. When I say access, what I mean is if we have this array with three items called `names`, then I ask for `names[2]`, it's constant time to give me `"Andre"`. A misconception that I've seen a lot of people have is that when you have a 10,000 element array and you ask for the 9000th element - let's say JavaScript isn't going through every single element in counting all the way up to 9000 and accessing every element and then getting to the one you need and giving it to you. You can think of there's a direct shortcut to each element if you have a number, if you have an index and the array goes that far, of course, that's the one condition, it's a valid index. You can jump immediately to the data. It doesn't matter how long the array is, or if you're looking at the last item, the middle item or the first item, it's constant time. 

So now that that's out of the way, let's talk about insertion and removal. It really depends on where we're inserting. Let's start with insertion, and it has to do with this order. As I've mentioned, each element has an index that corresponds to it. And if I want to add something in, let's say I want to add in the name `"Raj"`, And I add it to the very end, like right here by pushing onto this array that is constant time, O(1). We can add to the end of the array and we give it a new index. It's sort of like adding into an object, it's constant time, super simple, it doesn't require much work. The problem comes when we try and insert at the beginning of an array, and the reason for that has to do with these indices. If I tried to insert `Raj` at the very top, our indices are totally messed up. 
```JS
let names = ["Raj", "Michael", "Melissa", "Andrea"];
// ========== ^ =
// * Inserted   *
// ==============
```
`Michael` is no longer element 0, `Melissa` is not element 1, `Andrea` is not element 2. So we have to re index every single element in the array. This is simple for a four-element array, but if we're talking about thousands and thousands of elements re-indexing every single one is not a trivial task. So if we're inserting at the beginning of an array, we're talking about O(n) time because we have to do something once, roughly, for every single element. Now that doesn't mean that it's exactly one operation for each element. Remember O(n) could be O(10n), O(2n). And it's just that the amount of time it takes roughly grows in proportion with the size of the array. Inserting at the beginning is problematic. The same goes for removing from the beginning. Adding and removing from the beginning of an array is best to avoid if you can, but often it's meaningful to add to the beginning of an array. If you're trying to put something at the beginning of an order, for example, you may need to. 
>[!info]
>I'm not saying you should avoid it at all costs. It's just good to be aware that it's not as efficient.

It's adding in removing at the end. So `push` and `pop` always faster than `shift` and `unshift`. Unless of course it's an empty array, in which case adding to the beginning or end is the same thing. 

Always, inserting and removing from the beginning is worse than inserting to the end and removing from the end. Accessing is fast no matter where, if we're talking about 10,000 elements, accessing the middle element is just as fast as accessing the second element, and then searching... The fastest we can do is O(n). We'll discuss this in the searching section. We'll write our own basic JavaScript search. If we're talking about an unsorted array where there's no order to the data and I had, let's say, another 10,000 names in here and I wanted to know if `Ruby` was in there, we have to check potentially every single element. So as the number of items grows in that array, so does the time potentially that it takes to find that item. So search grows. Oh, again, it's a linear and we spend a lot more time talking about search and potential optimizations you can make specifically when your data is sorted, but that comes up later. All right. So next, we'll talk about some built in array methods and their performance.