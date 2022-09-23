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
## **Use cases in data files**
## **References**

\pagebreak
## Iterators
Basically, an iterator is an object which is used to iterate over items. In Python, an iterator is an object/class containing a countable number of elements and which implements the iterator protocols. In order to remember its current state during iteration, an iterator need an initialized iterable. Iterables are objects whose items can be looped over. For example, in Python we have collections like lists, tuples, strings, dictionnaries, sets... and classes containing the iterator protocols called magic or dunder methods. The iterator protocols consist of \_\_iter\_\_() and \_\_next\_\_() methods. The initialization process of the iterable is done using the \_\_iter\_\_() method. It returns the iterator itself. An iterable always has a \_\_iter\_\_() method.\
**Example 1**\
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
**Example 2**\
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
Iterators have both \_\_next\_\_() and \_\_iter\_\_() methods. Iterators are also iterables which are their own iterators. The only difference with collections is that iterators do not have length.\
**Example 3**\
code:\
```python
mydico = {"1":"Hello", "2":[1, 4, "foo"], "3":(6,8,3,)}
iterator = iter(mydico.values())
print(len(iterator))
```
Output:\
```python
File "c:\Users\user\Desktop\DIT\Python\literate-pancake\myExamples.py", line 48, in <module>
  print(len(iterator))
TypeError: object of type 'dict_valueiterator' has no len()
```
Now let add some examples to explore the iteration process.\
**Example 4**\
code:\
```python
# Return an iterator from a dictionary and print some values
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
The error is due to the fact that the next method were called a number of times greater than the length of the object. Then, it goes throgh all items and returns an error once there is not anymore value. To avoid that, one can define a condition or uses the StopIteration statement to stop the iteration once the iterations are complete.\
**Example 5**\
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
**Example 6**\
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
Some iterators do not do anything until we ask them to act. They are called generators or lazy iterators.\

\pagebreak
## Generators
In python, generators are lazy iterators that yield one item of a collection and waiting until the next item is required. They are used to control the iteration of a loop by suspending and resuming the process. Generators create iterators and iterables. Generators can be compiled in two forms: the generator methods and generator expressions.\
1. Generator methods
 A generator method is defined as a python method that uses the keyword 'yield' instead of the keyword 'return' that is mostly used by normal python methods.The 'return statement' in python exit from the code while the 'yield statement' stands by the running process at the current item and resumes it when the next item is needed. So, yielding a value means that the generator method gives the next item of the collection based on its current state and suspends the execution until the following value is needed. Thus, generator methods are also called suspendable or resumable methods. The object yielded by the generator method is called a generator object. It is obtained using \_\_next\_\_() method or a for loop. Therefore, a generator method is an iterator and a generator object is an iterable.\
**Example 7**\
Code:\
```python
def myFirstGen():
    yield "foo"
    yield "bar"
    yield "baz"
```

**Example 8**\
Still using the example above, we create the following iterable.\
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
# Using a 'for' loop
myString = myFirstGen()
for i in myString:
  print(i)
```
Output:\
```python
foo
bar
baz
```
2. Generator expressions\
Generator expressions are a mix of iterators and python list comprehensions. They provide syntactic sugar for writing generator methods or class iterators in a beautiful single-line of code. A generator expression does not contain the 'yield' keyword. A difference between list comprehensions and generator expressions is that list comprehensions returns all items of the list while the generator expressions yield one value at a time. In addition, the list comprehension statement is enclosed in square brackets while the generator expression is written in parentheses.\
**Example 9**\
This is a list comprehension\
```python
list_comprehension = ["hello world" for i in range(3)]
```
This is a generator expression\
```python
gen_expression = ("hello world" for in range(3))
```
For both generator methods and genarator expressions, the generator object is only evaluated when it is needed for use not when it is created. That means they yield one value at a time rather than storing all of them in memory. Thanks to the generators, the memory size will never change whatever the number of iterations.\

**Example 10**\
Let compare the size of a list myList and the size of the generator "range"\
Code:\
```python
import sys
# Using a list
myList = [0, 1, 2, 3, 4]
print("The memory size of the list my List is: ", sys.getsizeof(myList))

# Using the generator 'range'
print("The memory size using the range is: ", sys.getsizeof(range(5)))
```
Output:\
```python
The memory size of the list my List is:  120
The memory size using the range is:  48
```
The size of memory when using the generator "range" is less because instead of storing values in memory, it yields them only when needed. Therefore, its size will not change even if the number of iterations increases.\
**Example 11**\
Let increase the size of a list myList and the size of the generator 'range'\
Code:\
```python
import sys
# Using a list
myList = [0, 1, 2, 3, 4, 5, 6,7, 8, 9, 10]
print("The memory size of the list my List is: ", sys.getsizeof(myList))

# Using the genrator 'range'
print("The memory size using the range is: ", sys.getsizeof(range(100)))
```
Output:\
```python
The memory size of the list my List is:  152
The memory size using the range is:  48
```
Generator method can be written in a list comprehension form; it is called generator expression.\
**Example 12**\
Code:\
```python
genExp = (x*x for x in range(10))
print(genExp)
for i in genExp:
    print(i)
```
Output:\
```python
<generator object <genexpr> at 0x00000295DBF505F0>
0
1
4
9
16
25
36
49
64
81
```
\pagebreak
## Comparison between Iterators and Generators
Every generator is an iterator but every iterator is not a generator. There are several differences between iterators and generators. Iterators uses \_\_iter\_\_() and \_\_next\_\_() methods while generators uses the "yield" statement. Iterators are usually used to iterate or convert objects to get an iterator while generators are used in loops to generate an iterator. For a generator, local variables are stored before the yielding process. For an iterator, local variables are not used. Classes are used for iterators while methods are for generators.\


## Use cases in data files
Dealing with data in python can seem difficult when we fail to find a good way. When processing a simple collection of items, one can define single methods. However, data scientists face big data and then need a good approach to manipulate them. Therefore, writing single methods will give a code of hundred lines. That wastes time and becomes boring sometimes because there are a lot of workforce and brain activities. Thus, iterators and generators could give a way through a simple pipeline. Generators are most useful when working with textfiles or data streams. Their biggest achievement is that they can help processing large data files without storing the data in the RAM. We are going to give some examples of use-cases for generators as they can be considered as iterators too.\
**Example 13** Counting occurrence of words in textfile\
Code:\
```python
"""
Here, we are going to use generators to count 
the occurrence of each word in the textfile fileName
First of all the content of the textfile is opened line by line
not loaded all in memory
"""
file = open('fileName.txt', 'r') 
"""
The removeGen method go through the lines of the file and remove whitespaces using strip,
put all character in lowercase using lower method
and break each line into a list of word using split method
"""
def removeGen(file_handler):
    for row in file_handler:
        remove_ws = row.strip().lower().split()
        yield remove_ws
"""
We consider the word_count as a method that returns a dictionary with each word as
a key and its occurence as the value
"""       
def word_count(dict, key):
    dict[key] = dict.setdefault(key, 0) + 1

"""
We iterate using the generator method removeGen and use the word_count method
as a list comprehension to update the number of occurence.
When it is done, we close the file
"""  
w_count = {}
for row in removeGen(file):
    [ word_count(w_count, word) for word in row ]
file.close()
"""
Now print the results
"""
for row in sorted(w_count.items(), key=lambda x: x[1]):
    print(row[0], ': ', row[1])

```
Output:\
```python
words :  1
spread :  1
its :  1
magic :  1
and :  1
it :  1
offers :  1
a :  1
better :  1
life. :  1
quality :  1
is; :  1
actions :  1
speak :  1
of :  1
knowledge. :  1
bother :  1
people :  1
back; :  1
make :  1
them :  1
silent :  1
with :  1
work. :  1
all :  1
good :  1
things :  1
will :  1
definitely :  1
knock :  1
door. :  1
let :  2
the :  2
on :  2
you :  2
do :  2
not :  2
say :  2
what :  2
your :  6
```
**Example 14**\
Code:\
```python
"""
Here, we open the csv file clients.csv and yield data per one single value using generator instead of storing all values at once
"""
import csv
file_handler = open('clients.csv','r')
"""
read_file method returns a list that contains each line of the csv file
The elements in the list block are not stored in memory, they are yielded only
when needed. 
"""
def read_file(file_handler):
    block = []
    for line in file_handler:
        block.append(line)
    if block:
        yield block
"""
Now, we go through the list to show all values
"""
with open('clients.csv') as file_handler:
    for block in read_file(file_handler):
        print(block)
```

\pagebreak
## References
https://www.geeksforgeeks.org/generators-in-python/  \
https://anandology.com/python-practice-book/iterators.html \
https://www.machinelearningplus.com/python/generators-in-python/ \
https://towardsdatascience.com/implementing-a-data-pipeline-by-chaining-python-iterators-b5887c2f0ec6
