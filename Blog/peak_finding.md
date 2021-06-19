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

- T(n) = The work of what the algorithm does on the input of size n

- Base case: T(1) = O(1) ... This is the work for a case of 1 element

- For our simple algorithm, let's expand it in detail!

- T(n) = O(1) + O(1) + O(1) + O(1) + O(1) + O(1) + O(1) + O(1) + O(1)

- That leaves us with a case of O(log<sub>2</sub>n), because in mathematics the binary logarithm is the power to which the number in the subscript (our case it is 2) must be raised to obtain the value of n.

> What's the difference between O(n) and O(log<sub>2</sub>n)?

*If we run n on ten million, our one-dimensional linear solution solves in an impressive 13 seconds, but the divide and conquer solution can solve the same data set in .001 seconds. Math Rocks!*


## **2D: Finding a Peak**


## Keep complexity in mind.