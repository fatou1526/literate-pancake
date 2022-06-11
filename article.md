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
In Python, an iterator is an object containing a countable number of elements and which implements the iterator protocols. The iterator protocols consist of \_\_iter\_\_() and \_\_next\_\_() methods. The \_\_iter\_\_() method returns the iterator itself. The \_\_next\_\_() method returns the next item in the sequence.\
An iterator always remembers its current state during iteration so that it can step forward the next value of the iterable. An iterator can be obtained from lists, tuples, strings, dictionnaries and sets.\
**Example 1** \
```python
# Return an iterator from a string and print some values

mystring = "Python is more than a snake"
myiter = iter(mystring)
print(next(myiter))
print(next(myiter))
print(next(myiter))
print(next(myiter))
print(next(myiter))
print(next(myiter))
print(next(myiter))
print(next(myiter))

```
**Example 2**
```python
#return an iterator from a dictionnary and print some values
mydico = {"1":"Hello", "2":[1, 4, "foo"], "3":(6,8,3,)}
myiter = iter(mydico)
print(next(myiter))
print(next(myiter))
print(next(myiter))
```
**Notice**
From the examples, we can see that the \_\_next\_\_() method would continue as long as it is called. To avoid that, one can define a condition or uses the StopIteration statement to raise an error if the specified iterations number is done.
**Example 3**
```python
mystring = "foobarbaz"
myiter = iter(mystring)
while True:
  try:
    item = next(myiter)
    print(item)
  except StopIteration:
    break
```


