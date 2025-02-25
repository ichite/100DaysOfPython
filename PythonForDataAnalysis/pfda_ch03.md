# Chpater 3. Built-in Data Structures, Functions, and Files

## 3.1 Data Structures and Sequences

### Tuple

Fixed-length, immutable sequence of Python objects.


```python
tup = 4, 5, 6
tup
```




    (4, 5, 6)




```python
nested_tup = (4, 5, 6), (7, 8)
nested_tup
```




    ((4, 5, 6), (7, 8))



Can convert a sequence or iterator to a tuple with the `tuple` function.


```python
tuple([4, 0, 2])
```




    (4, 0, 2)




```python
tuple('string')
```




    ('s', 't', 'r', 'i', 'n', 'g')



Indexing a tuple is standard.


```python
tup[1]
```




    5



While the tuple is not mutable, mutable objects within the tuple can be modified in place.


```python
tup = 'foo', [1, 2], True
tup[1].append(3)
tup
```




    ('foo', [1, 2, 3], True)



Tuples can be concatenated using the `+` operator or repeated with the `*` operator and an integer.
Note that the objects are not copied, just the references to them.


```python
(4, None, 'foo') + (6, 0) + ('bar', )
```




    (4, None, 'foo', 6, 0, 'bar')




```python
('foo', 'bar') * 4
```




    ('foo', 'bar', 'foo', 'bar', 'foo', 'bar', 'foo', 'bar')




```python
tup = ([1, 2], 'foo')
tup = tup * 4
tup[0].append(3)
tup
```




    ([1, 2, 3], 'foo', [1, 2, 3], 'foo', [1, 2, 3], 'foo', [1, 2, 3], 'foo')



Tuples can be unpacked by position.


```python
tup = (4, 5, 6)
a, b, c = tup
b
```




    5




```python
tup = 4, 5, (6, 7)
a, b, (c, d) = tup
d
```




    7




```python
a, b = 1, 2
b, a = a, b
a
```




    2



A common use of variable unpacking is iterating over sequences of tuples or lists.


```python
seq = [(1, 2, 3), (4, 5, 6), (7, 8, 9)]
for a, b, c, in seq:
    print(f'a={a}, b={b}, c={c}')
```

    a=1, b=2, c=3
    a=4, b=5, c=6
    a=7, b=8, c=9


Another common use is return multiple values from a function (discuessed later).

There is specific syntax if you only want the first few values and put the rest into another tuple.


```python
values = tuple(range(5))
a, b, *rest = values
a
```




    0




```python
b
```




    1




```python
rest
```




    [2, 3, 4]



If you don't want the other values, the convention is to assign them to a variable called `_`.


```python
a, b, *_ = values
```


```python
a, b, *_ = values
```

### List

Variable-lengthed and the contents can be modified in place.


```python
a_list = [2, 3, 7, None]
a_list
```




    [2, 3, 7, None]




```python
tup = 'foo', 'bar', 'baz'
b_list = list(tup)
b_list
```




    ['foo', 'bar', 'baz']




```python
b_list[1]
```




    'bar'




```python
b_list[1] = 'peekaboo'
b_list
```




    ['foo', 'peekaboo', 'baz']



Elements can be added, inserted, removed, etc.


```python
b_list.append('dwarf')
b_list
```




    ['foo', 'peekaboo', 'baz', 'dwarf']




```python
b_list.insert(1, 'red')
b_list
```




    ['foo', 'red', 'peekaboo', 'baz', 'dwarf']




```python
b_list.pop(2)
```




    'peekaboo'




```python
b_list
```




    ['foo', 'red', 'baz', 'dwarf']




```python
b_list.append('foo')
b_list.remove('foo')
b_list
```




    ['red', 'baz', 'dwarf', 'foo']



Lists can be concatenated using the `+` operator.
Alternatively, an existing list can be extended using the `extend` method and passing another list.


```python
[4, None, 'foo'] + [7, 8, (2, 3)]
```




    [4, None, 'foo', 7, 8, (2, 3)]




```python
x = [4, None, 'foo']
x.extend([7, 8, (2, 3)])
x
```




    [4, None, 'foo', 7, 8, (2, 3)]



A list can be sorted in place.


```python
a = [7, 2, 5, 1, 3]
a.sort()
a
```




    [1, 2, 3, 5, 7]



Sort has a few options, one being `key` that allows us to define the function used for sorting.


```python
b = ['saw', 'small', 'He', 'foxes', 'six']
b.sort(key=len)
b
```




    ['He', 'saw', 'six', 'small', 'foxes']



The 'bisect' module implements binary search and insertion into a sorted list.
This finds the location of where to insert a new element to maintain the sorted list.
`bisect.bisect(list, value)` finds the location for where the element should be added, `bisect.insort` actually inserts the element.


```python
import bisect
c = [1, 2, 2, 2, 2, 3, 4, 7]
bisect.bisect(c, 2)
```




    5




```python
bisect.bisect(c, 5)
```




    7




```python
bisect.insort(c, 6)
c
```




    [1, 2, 2, 2, 2, 3, 4, 6, 7]



Specific elements of a list can be accessed using *slicing*.


```python
seq = [7, 2, 3, 7, 5, 6, 0, 1]
seq[1:5]
```




    [2, 3, 7, 5]




```python
seq[3:4] = [6, 7, 8, 9]
```


```python
seq
```




    [7, 2, 3, 6, 7, 8, 9, 5, 6, 0, 1]




```python
seq[:5]
```




    [7, 2, 3, 6, 7]




```python
seq[5:]
```




    [8, 9, 5, 6, 0, 1]




```python
seq[-4:]
```




    [5, 6, 0, 1]




```python
seq[-6:-2]
```




    [8, 9, 5, 6]



A step can also be included after another `:`.


```python
seq[::2]
```




    [7, 3, 7, 9, 6, 1]




```python
seq[::-1]
```




    [1, 0, 6, 5, 9, 8, 7, 6, 3, 2, 7]



### Built-in sequence functions

There are a number of useful built-in functions specifically for sequence types.

`enumerate` builds an iterator of the sequence to return each value and its index.


```python
some_list = ['foo', 'bar', 'baz']
for i, v in enumerate(some_list):
    print(f'{i}. {v}')
```

    0. foo
    1. bar
    2. baz


`sorted` returns a *new* sorted list from the elements of a sequence.


```python
sorted([7, 1, 2, 6, 0, 3, 2])
```




    [0, 1, 2, 2, 3, 6, 7]




```python
sorted('horse race')
```




    [' ', 'a', 'c', 'e', 'e', 'h', 'o', 'r', 'r', 's']



`zip` pairs up elements of a number of sequences to create a list of tuples.


```python
seq1 = ['foo', 'bar', 'baz']
seq2 = ['one', 'two','three']
zipped = zip(seq1, seq2)
list(zipped)
```




    [('foo', 'one'), ('bar', 'two'), ('baz', 'three')]




```python
seq2 = ['one', 'two']
list(zip(seq1, seq2))
```




    [('foo', 'one'), ('bar', 'two')]




```python
for a, b in zip(seq1, seq2):
    print(f'{a} - {b}')
```

    foo - one
    bar - two


A list of tuples can also be "un`zip`ped".


```python
pitchers = [
    ('Nolan', 'Ryan'),
    ('Roger', 'Clemens'),
    ('Curt', 'Schilling')
]
first_names, last_names = zip(*pitchers)
first_names
```




    ('Nolan', 'Roger', 'Curt')




```python
last_names
```




    ('Ryan', 'Clemens', 'Schilling')



The `reversed` function iterates over the sequence in reverse order.


```python
list(reversed(range(10)))
```




    [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]



### Dictionaries

A flexibly-sized collection of *key-value* pairs.


```python
empty_dict = {}
d1 = {'a': 'some value', 'b': [1, 2, 3, 4]}
d1
```




    {'a': 'some value', 'b': [1, 2, 3, 4]}




```python
d1[7] = 'an integer'
d1
```




    {'a': 'some value', 'b': [1, 2, 3, 4], 7: 'an integer'}




```python
d1['b']
```




    [1, 2, 3, 4]



You can check if a key is in a dictionary.


```python
'b' in d1
```




    True



A key-value pair can be deleted using `del` or the `pop` method which returns the value.


```python
d1[5] = 'some value'
d1
```




    {'a': 'some value', 'b': [1, 2, 3, 4], 7: 'an integer', 5: 'some value'}




```python
del d1[5]
```


```python
d1
```




    {'a': 'some value', 'b': [1, 2, 3, 4], 7: 'an integer'}




```python
ret = d1.pop('a')
d1
```




    {'b': [1, 2, 3, 4], 7: 'an integer'}




```python
ret
```




    'some value'



The `keys` and `values` methods return iteractors of the dictionary's keys and values.
While they do not return in a particular order, they *do* return in the same order.


```python
list(d1.keys())
```




    ['b', 7]




```python
list(d1.values())
```




    [[1, 2, 3, 4], 'an integer']



A dictionary can be added to another using the `update` method.


```python
d1.update({'b': 'foo', 'c': 12})
d1
```




    {'b': 'foo', 7: 'an integer', 'c': 12}



We will learn about dictionary comhrehensions later, but for now, here is a good way to contruct a dictionary from two lists or tuples.


```python
mapping = dict(zip(range(5), reversed(range(5))))
mapping
```




    {0: 4, 1: 3, 2: 2, 3: 1, 4: 0}



The `get` and `pop` methods for dicitonary can take default values for if the key does not exist in the dictionary.


```python
words = ['apple', 'bat', 'bar', 'atom', 'book']
by_letter = {}
for word in words:
    letter = word[0]
    if letter not in by_letter:
        by_letter[letter] = [word]
    else:
        by_letter[letter].append(word)

by_letter
```




    {'a': ['apple', 'atom'], 'b': ['bat', 'bar', 'book']}



This can instead be written more concisely as follows.


```python
by_letter = {}
for word in words:
    letter = word[0]
    by_letter.setdefault(letter, []).append(word)

by_letter
```




    {'a': ['apple', 'atom'], 'b': ['bat', 'bar', 'book']}



### Set

An unordered collection of *unique* elements - the name comes from the mathematical term.


```python
set([1, 1, 2, 3, 4, 4, 5, 6, 6])
```




    {1, 2, 3, 4, 5, 6}




```python
{1, 1, 2, 3, 4, 4, 5, 6, 6}
```




    {1, 2, 3, 4, 5, 6}



Sets support standard set operations such as union, intersection, difference, and symmetric difference.


```python
a = {1, 2, 3, 4, 5}
b = {3, 4, 5, 6, 7, 8}
a.union(b)
```




    {1, 2, 3, 4, 5, 6, 7, 8}




```python
a | b
```




    {1, 2, 3, 4, 5, 6, 7, 8}




```python
a.intersection(b)
```




    {3, 4, 5}




```python
a & b
```




    {3, 4, 5}




```python
a - b
```




    {1, 2}




```python
b - a
```




    {6, 7, 8}




```python
a ^ b
```




    {1, 2, 6, 7, 8}




```python
a.issubset(b)
```




    False




```python
a.issuperset({1, 2, 3})
```




    True



### List, set, and dictionary comprehensions

These are features for the easy (and fast) creation of the collection types.
The basic format is as follows

`[` *expr* `for` *val* `in` *collection* `if` *condition* `]`

This is equivalent to the following loop.

```python
result = []
for val in collection:
    if condition:
        result.append(expr)
```

The condition can be omitted if no filter is needed.


```python
strings = ['a', 'as', 'bat', 'car', 'dove', 'python']
[x.upper() for x in strings if len(x) > 2]
```




    ['BAT', 'CAR', 'DOVE', 'PYTHON']



A dicitonary comprehension is syntactically simillar.

`{` *key-expr* `:` *value-expr* for *value* in *collection* `if` *condition*}

A set comprehension is identical to a list comprehension save for it uses curly braces instead of square brackets.


```python
{val : index for index, val in enumerate(strings)}
```




    {'a': 0, 'as': 1, 'bat': 2, 'car': 3, 'dove': 4, 'python': 5}



List comprehensions can be nested.
Here is one example where a list of two lists are iterated over and only the names with at least two 'e's are kept.


```python
 all_data = [
     ['John', 'Emily', 'Michael', 'Mary', 'Steven'],
     ['Maria', 'Juan', 'Javier', 'Natalia', 'Pilar']
]
[name for names in all_data for name in names if name.count('e') >= 2]
```




    ['Steven']



The next example is followed by an identical nested `for` loop.
Notice that the order of the `for` expressions are the same.


```python
some_tuples = [(1, 2, 3), (4, 5, 6), (7, 8, 9)]
[x for tup in some_tuples for x in tup]
```




    [1, 2, 3, 4, 5, 6, 7, 8, 9]




```python
flattened = []
for tup in some_tuples:
    for x in tup:
        flattened.append(x)
flattened
```




    [1, 2, 3, 4, 5, 6, 7, 8, 9]



## 3.2 Functions


```python
def my_function(x, y, z=1.5):
    if z > 1:
        return z * (x + y)
    else:
        return z / (x + y)
```


```python
my_function(5, 6, z=0.7)
```




    0.06363636363636363



Note that there are various ways to pass arguments to functions that are not covered here with several new ones available in Python 3.8.

### Namespaces, scope, and local functions

A function gets its own *local* namespace when it is called, this is immediately populated with the arguments, and it is destryoed once the function returns.
A global variable can be created using the `global` keyword.


```python
a = None
a
```


```python
def bind_a_variable():
    global a
    a = []

bind_a_variable()
print(a)
```

    []


### Returning multiple values

Functions can only return one object, but by returning a tuple, unpacking can be used to create multiple variables.


```python
def f():
    a = 5
    b = 6
    c = 7
    return a, b, c

a, b, c = f()
print(f"a={a}, b={b}, c={c}")
```

    a=5, b=6, c=7


Another option is to use a dictionary.
This allows for the naming of the returned values.

### Functions are objects

Say we wanted to clean the input from a survey.


```python
states = ['    Alabama', 'Georgia!', 'Georgia', 'georgia', 'flOrIda', 'south   carolina###', 'West virginia?']
```

We could use one function to implement various string methods and methods from 're' for regular expressions.


```python
import re

def clean_strings(strings):
    result = []
    for value in strings:
        value = value.strip()
        value = re.sub('[!#?]', '', value)
        value = value.title()
        result.append(value)
    return result

clean_strings(states)
```




    ['Alabama',
     'Georgia',
     'Georgia',
     'Georgia',
     'Florida',
     'South   Carolina',
     'West Virginia']



Alternatively, we could make a few functions that each do one step in the processing and apply it to all of the values of a list.


```python
def remove_punctuation(value):
    return re.sub('[!#?]', '', value)

cleaning_operations = [str.strip, remove_punctuation, str.title]

def clean_strings(strings, ops):
    result = []
    for value in strings:
        for function in ops:
            value = function(value)
        result.append(value)
    return result

clean_strings(states, cleaning_operations)
```




    ['Alabama',
     'Georgia',
     'Georgia',
     'Georgia',
     'Florida',
     'South   Carolina',
     'West Virginia']



### Anonymous (lambda) functions

Thesse are single-line functions that autmatcially return the final value.
They are defined by the keyword `lambda`.
These are very useful in data analysis for passing a function as an argument to another function.


```python
anon = lambda x: x * 2
anon(3)
```




    6




```python
def apply_to_list(some_list, f):
    return [f(x) for x in some_list]

ints = [4, 0, 1, 5, 6]
apply_to_list(ints, lambda x: x * x)
```




    [16, 0, 1, 25, 36]



Another example is where some common methods take functions for an argument to augment their default functionality.


```python
strings = ['foo', 'card', 'bar', 'aaaa', 'abab']
strings.sort(key = lambda x: len(set(list(x))))
strings
```




    ['aaaa', 'foo', 'abab', 'bar', 'card']



### Currying: partia argument application

*Currying* is a CS term that means deriving new functions from existing once by *partial argument application*.
For example, `add_numbers` adds its two paramters, `x` and `y` together.
It is *curried* by `add_five` which sets `x` to be 5, automatically.


```python
def add_numbers(x, y):
    return x + y

add_five = lambda y: add_numbers(5, y)
```

### Generators

The *iterator protocol* is a generic way to make iterable objects.
An iterator object can specifically be created from most built-in collection types.


```python
dict_iterator = iter(d1)
dict_iterator
```




    <dict_keyiterator at 0x11c920a10>




```python
list(dict_iterator)
```




    ['b', 7, 'c']



The iterator yields the objects when it is used in a `for`-like context or passed to the common built-in methods that take collection types.

A *geerator* is a way to create a new iterable object.
They are like functions, but return multiple objects in a lazy fashion.
A generator is created using the `yield` keyword instead of a `return`.


```python
def squares(n=10):
    print(f'Generating squares from 1 to {n}.')
    for i in range(1, n + 1):
        yield i**2

gen = squares() 
```


```python
gen
```




    <generator object squares at 0x11da31bd0>




```python
for x in gen:
    print(x, end = ' ')
```

    Generating squares from 1 to 10.
    1 4 9 16 25 36 49 64 81 100

Generators can be created using a *generator expression* which is simillar in kind and syntax to list comprehensions.


```python
gen = (x**2 for x in range(100))
gen
```




    <generator object <genexpr> at 0x11db32ed0>




```python
sum(gen)
```




    328350



The `itertools` module from the standard library has a collection of generators for many common data algorithms.
Here is an example of `groupby`.


```python
import itertools

first_letter = lambda x: x[0]

names = ['Alan', 'Adam', 'Wes', 'Will', 'Albert', 'Steven']

for letter, names in itertools.groupby(names, first_letter):
    print(letter, list(names))

```

    A ['Alan', 'Adam']
    W ['Wes', 'Will']
    A ['Albert']
    S ['Steven']


### Errors and exception handling

Use `try-except` to fail gracefully.


```python
def attempt_float(x):
    try:
        return float(x)
    except:
        return x

attempt_float('1.23')
```




    1.23




```python
attempt_float('a')
```




    'a'



You can define `except` for different types of errors.
For example, when `float()` is passed an improper string, it raises a `ValueError`.
If it is passed a tuple, it raises a `TypeError`.


```python
attempt_float((1, 2))
```




    (1, 2)




```python
def attempt_float(x):
    try:
        return float(x)
    except ValueError:
        print('value error')
    except TypeError:
        print('type error')
```


```python
attempt_float(5)
```




    5.0




```python
attempt_float('a')
```

    value error



```python
attempt_float((2, 3))
```

    type error


A single `except` can recognize multiple error types.


```python
def attempt_float(x):
    try:
        return float(x)
    except (TypeError, ValueError):
        return x
```

Often, you want some code to execute after a command regardless of whether it succeeds or fails.


```python
def attempt_float(x):
    try:
        return float(x)
    except ValueError:
        print('error')
        return x
    else:
        print('succeeded')
    finally:
        print('all done')
```


```python
attempt_float(1)
```

    all done





    1.0




```python
attempt_float('a')
```

    error
    all done





    'a'



## 3.3 Files and the operating system

Open a file for reasing using the `open` function.


```python
path  = "assets/segismundo.txt"
f = open(path)
```

It is opened in a 'read-only' form, by default.
Lines can be iterated through.


```python
for line in f:
    print(line)
```

    Sueña el rico en su riqueza,
    
    que más cuidados le ofrece;
    
    
    
    sueña el pobre que padece
    
    su miseria y su pobreza;
    
    
    
    sueña el que a medrar empieza,
    
    sueña el que afana y pretende,
    
    sueña el que agravia y ofende,
    
    
    
    y en el mundo, en conclusión,
    
    todos sueñan lo que son,
    
    aunque ninguno lo entiende.
    


It is important to close files that are opened.


```python
f.close()
```

It is often useful to remove end-of-line markers.


```python
lines = [x.rstrip() for x in open(path)]
lines
```




    ['Sueña el rico en su riqueza,',
     'que más cuidados le ofrece;',
     '',
     'sueña el pobre que padece',
     'su miseria y su pobreza;',
     '',
     'sueña el que a medrar empieza,',
     'sueña el que afana y pretende,',
     'sueña el que agravia y ofende,',
     '',
     'y en el mundo, en conclusión,',
     'todos sueñan lo que son,',
     'aunque ninguno lo entiende.']



Alternatively, it is often easier to use a `with` statement that autmatcially cleans up the open file when it finishes.


```python
with open(path) as f:
    lines = [x.rstrip() for x in f]
```

For readable files, a few commonly used methods are:

- `read`: returns a certain number of characters from a file
- `seek`: changes the file position to the indicated byte
- `tell`: gives the current position  in the file


```python
f = open(path)
f.read(10)
```




    'Sueña el '




```python
f2 = open(path, 'rb')  # binary mode
f2.read(10)
```




    b'Suen\xcc\x83a el'




```python
f.tell()
```




    11




```python
f2.tell()
```




    10




```python
f.seek(3)
```




    3




```python
f.read(1)
```




    'n'




```python
f.close()
f2.close()
```

Use `write` or `writelines` to write to a file.


```python
with open('assets/tmp.txt', 'w') as handle:
    handle.writelines(x for x in open(path) if len(x) > 1)
```


```python
with open("assets/tmp.txt") as f:
    lines = f.readlines()

lines
```




    ['Sueña el rico en su riqueza,\n',
     'que más cuidados le ofrece;\n',
     'sueña el pobre que padece\n',
     'su miseria y su pobreza;\n',
     'sueña el que a medrar empieza,\n',
     'sueña el que afana y pretende,\n',
     'sueña el que agravia y ofende,\n',
     'y en el mundo, en conclusión,\n',
     'todos sueñan lo que son,\n',
     'aunque ninguno lo entiende.\n']


