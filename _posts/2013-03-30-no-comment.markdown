---
layout: post
title: "No Comment"
date: 2013-03-30 14:36
comments: true
categories: 
- Programming
---
I was always taught in school to liberally apply comments to my code. For a long time, I
considering this practice a good one. I no longer do, however.

Before you write me off as a lame-o programmer, to illustrate why I feel this way, let's walkthrough 
some examples using an old favourite algorithm: merge sort. For the sake of this exercise, though, let's assume
that merge sort is not a widely known algorithm, so we don't fall into the *it's merge sort, duh!*
trap.

```
def mergesort(a):
	if len(a) <= 1:
		return a
	m = len(a) / 2
	l = a[:m]
	r = a[m:]
	return merge(mergesort(l), mergesort(r))

def merge(l, r):
	li = 0
	ri = 0
	m = []
	while li < len(l) and ri < len(r):
		if l[li] < r[ri]:
			m.append(l[li])
			li += 1
		else:
			m.append(r[ri])
			ri += 1
	if li < len(l):
		m.extend(l[li:])
	else:
		m.extend(r[ri:])
	return m
```

Here we have a completely correct sorting algorithm coded in one of my favourite languages, [Python](http://www.python.org/). 
In my opinion, though, correct code is not quite good enough. This code could be improved in some ways. 
Let's assume that liberally adding comments is one of these ways.

```
def mergesort(a):
	"""Returns a sorted list.
	"""
	# Base case for recursive algorithm is when
	# there is 1 or less elements. In either case, we call 
	# the list sorted.
	if len(a) <= 1:
		return a
	# Find the middle of the list
	m = len(a) / 2
	# Split the list into halves
	l = a[:m]
	r = a[m:]
	# Merge the two sorted halves 
	return merge(mergesort(l), mergesort(r))

def merge(l, r):
	"""Returns a merged sorted list.
	"""
	# Track the positions of the lists starting at index 0
	li = 0
	ri = 0
	# Initialize an empty list to store the final sorted list
	m = []
	# Loop while both halves still have unprocessed elements
	while li < len(l) and ri < len(r):
		# When the left list element is less than the right
		# list element, we add it to the final sorted list
		# and increment the position for the left side. Otherwise
		# we do it for the right side
		if l[li] < r[ri]:
			m.append(l[li])
			li += 1
		else:
			m.append(r[ri])
			ri += 1
	# Since one list has been completely processed, we extend
	# the final sorted list with the sorted elements remaining in
	# the other list
	if li < len(l):
		m.extend(l[li:])
	else:
		m.extend(r[ri:])
	return m
```

My once *Intro to Algorithms* professor would really like this version. But, you, however, *shouldn't* like this.
Let me explain.

Since I'm assuming that merge sort is an unknown algorithm, in an effort to improve readability, I've 
added *lots* of prologue comments. They basically reiterate *what the code is doing.* To me, these types of comments
add too much clutter and may over-complicate something that wasn't all that complicated to begin with (like in
this case). For a college professor receiving something like this from a student as an assignment, these comments
could be useful, as they could give insight into whether or not a student understands what the code is doing. 
However, in a work setting, it should be a fair assumption that your colleagues can **read the code to figure out 
what the code is doing**.

It could be argued, though, that without the prologue comments, the readability is suffering because the variable 
names don't convey enough about the code. That's a valid point. So, let's try something different.

```
def mergesort(unsorted):
	"""Returns a sorted list. 

	The passed list is recursively halved 
	into sublists until each sublist has one or less elements. Then, 
	the sublists are merged together such that their elements are in order.

	Worst case time complexity is O(n log n).
	Worst case space complexity is O(n).
	"""
	if len(unsorted) <= 1:
		return unsorted
	
	middle = len(unsorted) / 2
	left_half = unsorted[:middle]
	right_half = unsorted[middle:]
	
	return merge(mergesort(left_half), mergesort(right_half))

def merge(left, right):
	"""Returns a sorted list as a result of merging 
	two sorted lists.
	"""
	left_index = right_index = 0
	merged = []
	
	while left_index < len(left) and right_index < len(right):
		if left[left_index] < right[right_index]:
			merged.append(left[left_index])
			left_index += 1
		else:
			merged.append(right[right_index])
			right_index += 1
	
	left_remaining = left_index < len(left)
	if left_remaining:
		merged.extend(left[left_index:])
	else:
		merged.extend(right[right_index:])
	
	return merged
```

This version follows the **no comment is the best comment** approach. The variable names
have been modified (and according to [Python style guidelines](http://www.python.org/dev/peps/pep-0008/))
to convey their purpose making the code self-documenting and rendering all the prologue comments unnecessary.
**The code itself effectively describes _what the code is doing_**.

The function headers have been improved such that callers can discover what the functions do without reading
a single line of code. This is especially important for public interfaces and let's us use tools like [pydoc](http://docs.python.org/2/library/pydoc.html) to easily share code documentation.

You may be wondering, *what's the big deal? Let's just refactor and keep the comments too so we can have the 
best of both worlds!*
The problem is that adding unnecessary comments creates another set of things to maintain. It's even worse when
the code changes and the comments are orphaned. Suppose a colleague comes along and changes the code again based
on comments that incorrectly describe code that no longer exists. Now, things are really a mess. Then, 
your colleague goes on vacation and a bug surfaces related to all these changes and you're stuck `git bisect`'ing 
your way through it all to figure out where things went wrong! So, I'll state this again very explicity: liberal
code commenting is wasted effort; make your code more self-documenting because **no comment is the 
best comment**.
