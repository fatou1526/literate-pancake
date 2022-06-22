---
title: |
  **ITERATORS AND GENERATORS PROTOCOL IN PYTHON**
date: June, 2022
lang: en-EN
urlcolor: blue
geometry: "left=2.5cm,right=2.5cm,top=3cm,bottom=3cm"
documentclass: article
fontfamily: Alegreya
header-includes: |
    \usepackage{fancyhdr}
    \pagestyle{fancy}
    \fancyhf{}
    \rhead{Dakar Institute of Technology}
    \lhead{Ndeye Fatou Sene}
    \rfoot{Page \thepage}
    \hypersetup{pdftex,
            pdfauthor={Ndeye Fatou Sene},
            pdftitle={ITERATORS AND GENERATORS PROTOCOL IN PYTHON},
            pdfsubject={ITERATORS AND GENERATORS PROTOCOL IN PYTHON},
            pdfkeywords={Python, Iterators, Generators},
            pdfproducer={Emacs, Pandoc, Latex, Markdown},
            pdfcreator={Emacs, Pandoc, Latex, Markdown}}
    
---
# **WORK PLAN**
## **Iterators**
## **Generators**
## **Comparison between Iterators and Generators**
## **Practical cases**
## **Conclusion** 

\pagebreak
# Iterators
Basically, an iterator is an object which is used to iterate over items. In Python, an iterator is an object/class containing a countable number of elements and which implements the iterator protocols. In order to remember its current state during iteration, an iterator need an initialized iterable. Iterables are objects whose items can be looped over. For example, in Python we have lists, tuples, strings, dictionnaries, sets and classes containing the iterator protocols called magic or dunder methods. The iterator protocols consist of \_\_iter\_\_() and \_\_next\_\_() methods. The initialization process of the iterable is done using the \_\_iter\_\_() method. It returns the iterator itself. An iterable always has a \_\_iter\_\_() method.\
**Example 1**
Code:\
```python
# Check the presence of iter() method for an object of type dictionnary
mydico = {"1":"Hello", "2":[1, 4, "foo"], "3":(6,8,3,)}
print(dir(mydico))
```
Output:\
```python
['__class__', '__class_getitem__', '__contains__', '__delattr__', '__delitem__',
'__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__',
'__getitem__', '__gt__', '__hash__', '__init__', '__init_subclass__',
'__ior__', '__iter__', '__le__', '__len__', '__lt__', '__ne__',
'__new__', '__or__', '__reduce__', '__reduce_ex__', '__repr__',
'__reversed__', '__ror__', '__setattr__', '__setitem__', '__sizeof__',
'__str__', '__subclasshook__', 'clear', 'copy', 'fromkeys', 'get',
'items', 'keys', 'pop', 'popitem', 'setdefault', 'update', 'values']
```
We see that the \_\_iter\_\_() is in the list of the outputs meaning that each dictionnary is an iterable.\ 
The iterator has the \_\_next\_\_() method to iterate items. \_\_next\_\_() method creates an state for the iterator so that it can remember its current state each time. It always returns the next item in the iterable.\
**Example 2**
Still considering the dictionary above, we have:\
Code:\
```python
# Check the presence of next() method for the iterator
myiter = mydico.__iter__()  # same as myiter = iter(mydico)  
print(dir(myiter))
```
Output:\
```python
['__class__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__',
'__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', 
'__init_subclass__', '__iter__', '__le__', '__length_hint__',
'__lt__', '__ne__', '__new__', '__next__', '__reduce__', 
'__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__']
```
The iterator has both \_\_next\_\_() and \_\_iter\_\_() methods.
Now let add some examples to explore the iteration process.\
**Example 3**\
code:\
```python
#return an iterator from a dictionnary and print some values
mydico = {"1":"Hello", "2":[1, 4, "foo"], "3":(6,8,3,)}
myiter = iter(mydico.values())
print(next(myiter))
print(next(myiter))
print(next(myiter))
print(next(myiter))
```
Output:\
```python
Hello
[1, 4, 'foo']
(6, 8, 3)
Traceback (most recent call last):
  File "c:\Users\user\Desktop\DIT\Data collection\exercice\tester.py", line 6, in <module>
    print(next(myiter))
StopIteration
```
**Notice**\
The error is due to the fact that the next method were called a number of times greater than the length of the object. Then, it goes throgh all items and returns an error once there is not a value anymore. To avoid that, one can define a condition or uses the StopIteration statement to stop the iteration once the iterations are complete.\
**Example 4**\
Code:\
```python
# Stop iteration when the last element is reached.
mystring = "foobarbaz"
myiter = iter(mystring)
while True:
  try:
    item = next(myiter)
    print(item)
  except StopIteration:
    break
```
Output:\
```python
f
o
o
b
a
r
b
a
z
```
Let try to obtain an iterator using a class object.\
**Example 5**\
Code:\
```python
# An example using class object
class Interval:
  def __init__(self, lowest, highest):
    self.current = lowest - 1
    self.highest = highest
  def __iter__(self):
    return self
  def __next__(self):
    self.current += 1
    if self.current < self.highest:
      return self.current
    raise StopIteration
  for a in Interval(23, 30):
    print(a)
```
Output:\
```python
23
24
25
26
27
28
29
```
\pagebreak
# Generators
In python, there are generator methods and generator objects. A generator is a method that generates a value using the keyword yield. In this case, yield keyword replaces the return statement that is commonly used by a lot of python methods.\
**Example 6**\
Code:\
```python
def myFirstGen():
    yield "foo"
    yield "bar"
    yield "baz"
```
A generator object is the object yield by the generator method. The object is obtained by iterating using \_\_next\_\_() method or in a for loop. Thus, the generator method is an iterator and a generator object is an iterable.\
Therefore, python generators proceed to create iterators and iterables.\
**Example 7**\
From the example above, we create the following iterable.\
Code:\
```python
# Using the next method to yield the object    
myString = myFirstGen()
print(myString.__next__())
print(myString.__next__())
print(myString.__next__())
```
Output:\
```python
foo
bar
baz
```
Code:\
```python
# Using the a 'for' loop to yield the object    
myString1 = myFirstGen()
for i in myString1:
    print(i)
```
Output:\
```python
foo
bar
baz
```
Using generator to create iterators is called lazy evaluation process because the generator object is only evaluated when it is needed for use not when it is created. That means they yield one value at a time rather than store all of them in memory. Thanks to the generators, the memory size does never change whatever the number of iterations is.



