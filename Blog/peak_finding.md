# Peak Finding

**This is a great toy problem. It gets you thinking in an algorithmic way.**

---

## **1D: Finding a Peak**

---

*Problem Domain: A one dimensional version of peak finding runs on an array of numbers. In the visual below, see how our containers are numbered 1-9? Our goal is to find a peak.*

![visual_1](/images/visual_1.png)

*What is the definition of the peak we need to find? Since we never explained this within the problem domain, it makes an excellent follow up question when presented with a problem like this.*

> There are a few things to know about this linear array:

Position 2 is a peak if, and only if:

- b >= a    (These operators together mean greater than or equal to)
- b >= c

Position 9 is a peak if i >= h

> A straightforward solution to this problem is to start from the left, comparing the next numbers until both surrounding numbers are either less than or equal to the number we are comparing. That means that number is a peak.
> NOTE: There could be multiple peaks, or no peaks. A question like this needs more clarification!

*A tidbit for your best algorithmic future: create algorithms in a general way, just in case the problem domain changes!*

> The worst case complexity for a linear approach to this problem domain is O(n) because in the end you may have to look at every element in order to find the peak... it may be the last one!

*Define O(n): O is the complexity constant, and n is the number of elements. So if we had 77 elements, the worst case isn't so bad... but what if we had a trillion data elements to go through? This isn't too efficient!*

**How do we lower that complexity?**

> Let's break it up into smaller portion in a divide and conquer manner, and search recursively!

- First, let's break the elements in half, and look at the n/2 element. From our example n=9 so n/2 is the 5th element.

![visual 2](/images/visual_2.png)

- if a [n/2] is less than a [n/2 - 1] then we would only look at the left half for a peak

- else if a [n/2] is less than a [n/2 +1] then we would look right of n/2 for a peak

- if neither condition is met, then we are done as n/2 qualifies as a peak!

- Given the definition of a peak (an element that is more than the elements surrounding it), we can conclude the element qualifies as a peak if both surrounding elements are found to be less than the current element.

![visual 3](/images/visual_3.png)

> Complexity of the Algorithm

### ProTip: Keep complexity in mind

- T(n) = The work of what the algorithm does on the input of size n

- Base case: T(1) = O(1) ... This is the work for a case of 1 element

- For our simple algorithm, let's expand it in detail!

- T(n) = O(1) + O(1) + O(1) + O(1) + O(1) + O(1) + O(1) + O(1) + O(1)

- That leaves us with a case of O(log<sub>2</sub>n), because in mathematics the binary logarithm is the power to which the number in the subscript (our case it is 2) must be raised to obtain the value of n.

> What's the difference between O(n) and O(log<sub>2</sub>n)?

*If we run n on ten million, our one-dimensional linear solution solves in an impressive 13 seconds, but the divide and conquer solution can solve the same data set in .001 seconds. Math Rocks!*

## **2D: Finding a Peak**

*Let's expand upon our 1d peak finding, into a 2 dimensional array version.*

![2d visial](/images/2d_visual_1.png)

*Here you see we have rows, as in the 1d version, but now we add more elements and create columns as well.*

> Our definition of a peak here is the top of a hill. There can be multiple peaks, or no peaks.

> Let's take a look at the element a from the visual above. We have rows labeled as n, and columns as m.

>The element a is a 2d peak if, and only if:

- a >= d (here we use >+ to mean greater than or equal to)

- a >= b

- a >= c

- a >= e

> you see, all four touching elements of our peak should be lower than, or equal to our peak element.

### A Greedy Ascent Algorithm

*A greedy ascent algorithm picks a direction and follows that to find a peak. Typically you will start in the middle, look left. If it is greater than the element we are currently on we move there are continue looking, if it is less we will look to the right.*

> In this visual we start at 12, and as we look left the algorithm goes to the next element that is greater than or equal to. Following the green elements, you can see the algorithm passes on 9, since it is lower than the surrounding elements, but when it reaches 20 the red indicated a peak. The surrounding elements are all lower, so there is nowhere togo and we have an answer.

> ProNote: Remember to handle edges!

![Visual 2, greedy ascent](/images/2d_visual_2.png)

### Let's Look at it's complexity

*The worst case analysis of this algorithm: You may end up touching a large fraction of the elements.*

> A greedy ascent algorithm has an O(nm) complexity.

> Take a look at the visual again. At the worst case you will have to go through all the the (n) rows and (m) columns. In order to calculate how many elements that is, you must multiply the rows and columns to get the 2d matrix size.

> ProNote: If [n=m] your complexity can be stated better as [O(n<sup>2</sup>)]

## Finding a Solution

> Let's adjust our visual! We will use i for the rows, and j (we need a little baby math here to get the mid) for the columns.

![Visual 3](/images/2d_visual_3.png)

> You could start by finding a peak in the mid column, by using (i, j) as a start, but this leaves you lacking! 

> But Niix, it has a log(m) complexity! It can't be that bad?

> But what if there isn't a peak there, but in another element? You still need to find the peak overall! What if there were a million elements to go through? Wouldn't finding peaks of each row and comparing them take a long time? Let's find a more efficient solution.

> Look at the row 14 is on... if we did a 1d analysis of that row we would get 14 as a peak, but look! 15 being below it disqualifies it from being a peak. We need a better way.

### Let's look at our solution algorithm:

- Pick the middle column using [j=m/2]
- Find the global max on column j at (i, j)
- Compare (i, j-1), (i, j), (i, j+1) *This looks left and right of our current element*
- Pick the left column if (i, j-1) > (i, j) *We are looking for a greater element, and this works simularly for the right, just add 1 instead*
- If neither condition fires, it implies (i, j) is a 2d peak

> Our base case: When we have a single column, find the global max, and you are done. 

> Let's look at the Overall Complexity of this solution:

- T(n, m) accounts for what the algorithm does on input of a 2d array.

- O(n) is the global max of how many row elements you have.

- Put those together and you get T(n, m) = T(n, m/2) + O(n)

- Worst case, we have equal numbers of rows and columns. That would be like adding your global max together one at a time for as many elements as you have. 10 isn't alot, but a million would take awhile!

> Let's Simplify our complexity!

- How do you add an unknow number of elements together? Let me introduce you back to log! 

- Here is what the simplified complexity looks like for our 2d array:

- **T(n, m) = O(log<sub>2</sub>m)**

- That looks more like it! This is taking our algorithmic work operation[T(m, n)], making it the exponent of 2 *to account for each element of O(n)* and setting it equal to the number of columns.

### Thank you for making it this far! I hope I've help you understand a bit more about the working of peak finding in a 1d and 2d array. Happy Coding!
