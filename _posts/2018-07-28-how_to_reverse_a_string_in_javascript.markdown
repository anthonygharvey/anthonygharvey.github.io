---
layout: post
title:      "How to Reverse a String in JavaScript"
date:       2018-07-29 01:27:22 +0000
permalink:  how_to_reverse_a_string_in_javascript
---


![](https://anthonygharvey.com/assets/img/tools.jpg)

This article is about practicing different JavaScript functions and creating algorithms because it is important to practice in order to perform well in technical interviews.  This article will teach you several approaches to solving a common technical interview question, reversing a string.

Reversing a string in JavaScript may seem like a simple task, but there are several steps involved and, in the context of a technical interview, it provides opportunities to showcase your knowledge of JavaScript and trade-offs / edge cases considered.  It’s  practice to make sure you understand the problem and any constraints before beginning to write code.

Some of the constraints may be given to you upfront, such as: “Write an algorithm that reverses a string in place **without** using built-in functions like `.reverse()` or `.charAt()`.  It’s always a good idea to ask clarifying questions before jumping in and attempting to solve the problem.  In this case we’re asked to reverse a string.  Some questions we could ask include:

1. Are there any conditions for the string that will be passed?
2. Will the string contain regular or special characters?

Let’s start with the least amount of constraints and work our way up:

> Given a string input, return  a string with its characters in the reversed order of the input string.

With this challenge, we are not provided with any restrictions on the functions we can use.  We can also ask our clarifying questions if the string input will contain any special characters or if there are any conditions.  For this challenge, lets assume the answer is the input will only contain regular ASCII characters.

Now that we’ve asked our clarifying questions, you can restate the problem with the new information to buy yourself more time to think and get used to communicating your thought process out loud.  You could say something like:

> Given a string input of **only ASCII characters**, I want to create a function that returns a **new string** with its characters in the reverse order of the input string.  I want to return a new string because I want to avoid mutating the original string input

Now that you’ve restated the problem as you understand it based on the responses to your clarifying questions, this may be a good point to write some simple examples.

```
reverse('hello') === 'olleh'
reverse('world!') === '!dlrow'
reverse('JavaScript') === 'tpircSavaJ'
```

 Now that we understand the problem, the input and expected output, we can break it down into steps.

1. convert the string into an array with each character in the string as an element
2. reverse the order or the elements in the array
3. convert the reversed array back into a string
4. return the reversed string

```
function reverse(string) {
	let answer = string.split('') // step 1
	answer.reverse()  // step 2
	answer = answer.join('')  // step 3
	return answer  //step 4
}
```
<a href="https://gist.jsbin.com/anthonygharvey/241c2abc569b283149f6895909af3c3a" target="_blank">JSBin link</a>

Next we can test the function with the examples we created above, again communicating our thought process out loud by saying something like:

> Given a string `hello` as an input, the function would:
> 1. first split the string on each character, convert it an array with each character as an element and assign the array to the variable `answer`
> 2. reverse the order of the elements in the `answer` array
> 3. join the elements in the reversed `answer` array into a string and reassign it to the `answer` variable
> 4. return the `answer` variable, which is now a reversed string of the input

Now that the function works, we can refactor it to make it more DRY.

```
function reverse(string) {
	return string.split('').reverse().join('')
}
```
<a href="https://gist.jsbin.com/anthonygharvey/42b7f1a4aa57a3c2f054172056da1083" target="_blank">JSBin link</a>

We can also use the <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax" target="_blank">spread syntax</a> inside of the array literal notation as an alternative to the `.split()` function.

```
function reverse(string) {
	return [...string].reverse().join('')
}
```
<a href="https://gist.jsbin.com/anthonygharvey/0d7e465ccfff6f7db027237babc17fd4" target="_blank">JSBin link</a>

Now lets suppose we’re given the same problem but with more constraints

> Given a string input, return  a string with its characters in the reversed order of the input string without using built-in functions like `.reverse()`, `.charAt()`, the spread syntax; and without using an array.

For the sake of brevity, lets assume the same answers to our clarifying questions above.  We can use the same approach for the first problem, but just with different steps given the new constraints.

1. create a variable to serve as the return value and set it as an empty string, call it `reversed`
2. loop through the characters in the input string
3. Within each loop iteration, add the character to the **beginning** of the `reversed` string
4. return `reversed`

The reason we want to add each character to the beginning of the `reversed` string is because if we added them to end of the string, we’d just be reconstructing the input string as is and we want the return value to be a reversed string.

```
function reverse(string) {
	let reversed = ''  // step 1
	for(let char of string) {  // step 2
		reversed = char + reversed;  // step 3
	}
	return reversed;  // step 4
}
```
<a href="https://gist.jsbin.com/anthonygharvey/2fe6dfce8b9fa72bc8223510f0175e59" target="_blank">JSBin link</a>

In step 3 we’re just concatenating the character in each iteration with the reversed string, (being careful to add it to the beginning) and reassigning the concatenated string back to the reversed variable.  In other words, starting with the character and adding (concatenating) the reversed string to the end of it; then reassigning this combined string to the `reversed` variable.  If we put `reversed = reversed + char`, that would be the opposite of what we want and would just reconstruct the input string (`reverse('hello') === 'hello'`).

![](https://anthonygharvey.com/assets/img/reverse_string_concatenation.png)

Also, step 2 uses the `for...of` statement introduced in ES2015.  The syntax is easier to read and it creates a loop that iterates over iterable objects.  If the interviewer asks you to not use ES2015, you can always use a the traditional `for` loop, but if you don’t have that restriction I think using `for...of` loops are better because the syntax is simpler and reduces the chances of unintentional errors being introduced (like using a comma instead of a semi-colon to separate the initial expression, condition and incremental expression).

For our last challenge, lets suppose we’re given the same problem, but the input strings may contain more than just ASCII characters.

>Given a string input of Unicode characters , return  a string with its characters in the reversed order of the input string.

In this challenge, the input string will be be more than 7 bit ASCII characters and contain 8 bit Unicode characters (see this <a href ="https://www.youtube.com/watch?v=5aJKKgSEUnY" target="_blank"> for a great explanation of the differences between ASCII and Unicode)</a>.

If we use our initial function to reverse a string containing Unicode characters, we get weird and unexpected results.  Let’s include an emoji in the string because, why not?!

```
function reverse(string) {
	return string.split('').reverse().join('')
}

reverse('JS is fun! 😄')
// => �� !nuf si SJ
```
<a href="https://gist.jsbin.com/anthonygharvey/4148ac0d8ac7434b0dbb27e734fefc09" target="_blank">JSBin link</a>

We can get around this by using the `Array.from()` method to create a new array from an array-like or iterable object (in our case a string).
```
function reverse(string) {
	return Array.from(str).reverse().join("")
}

reverse('JS is fun! 😄')
// => 😄 !nuf si SJ
```
<a href="https://gist.jsbin.com/anthonygharvey/09a6dd43beb7508aefebac9abdcc9ac1" target="_blank">JSBin link</a>

## Conclusion
Now that you’ve learned about different ways to approach the reverse a string algorithm problem in JavaScript, take a look at:
- <a href="https://medium.freecodecamp.org/10-common-data-structures-explained-with-videos-exercises-aaff6c06fb2b" target="_blank">10 Common Data Structures Explained with Videos + Exercise</a>
- <a href="https://dev.to/t/basecs" target="_blank">BaseCS Video Series</a>
- <a href="https://www.codenewbie.org/basecs" target="_blank">BaseCS podcast on CodeNewbie</a>

For more reading, checkout algorithm tutorials on <a href="https://coderbyte.com/challenges?a=true" target="_blank">Coderbyte</a> and the sorting algorithms animations by <a href="https://www.toptal.com/developers/sorting-algorithms" target="_blank">Toptal</a>.

I hope this was helpful!  Let me know if you have any questions or comments.  You can follow me on <a href="https://www.linkedin.com/in/anthonygharvey" target="_blank">LinkedIn</a>, <a href="https://github.com/anthonygharvey" target="_blank">GitHub</a>, <a href="https://twitter.com/anthonyharvey" target="_blank">Twitter</a> and on my <a href="https://anthonygharvey.com" target="_blank">my website</a>.
