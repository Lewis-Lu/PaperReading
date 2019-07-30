# Note Book
*Written by **Lewis***

## Native datatype

### List
* difference between append() and extend(). On the other hand, the append() method takes a single argument, which can be any datatype. Here, you’re calling the append() method with a list of three items.
The extend() method takes a single argument, which is always a list, and adds each of the items of that list to a_list.

* a = [1,2,3 'a'], a.index('c') will raise 'ValueError' instead of -1 like most other programming language. since -1 is a valid slice in python

* empty lists are false, all others are true

### Tuple
* A tuple is an **immutable** list. A tuple can not be changed in any way once it is created.

* define tuple in parentheses a = ('a', 'b')

* So what are tuples good for? 
    * Tuples are faster than lists. If you’re defining a constant set of values and all you’re ever going to do with it is iterate through it, use a tuple instead of a list.
    * It makes your code safer if you “write-protect” data that doesn’t need to be changed. Using a tuple instead of a list is like having an implied assert statement that shows this data is constant, and that special thought (and a specific function) is required to override that.
    * Some tuples can be used as dictionary keys, as you’ll see later in this chapter. (Lists can never be used as dictionary keys.)

* To create a tuple of one item, you need a comma after the value. (False,) is a tuple, (False) is boolean.

* in Python, you can use a tuple to assign multiple values at once.
v = ('a', 2, True)
(x, y, z) = v

### Set
* A set is an **unordered** “bag” of unique values. A single set can contain values of any datatype.

* To create an empty set, call set() with no arguments.
a_set = set()
type(a_set) = <class 'set'>

* Sets are bags of unique values. If you try to add a value that already exists in the set, it will do nothing. It
won’t raise an error; it’s just a no-op.

* a_set.update({1,2})
a_set.update([1,2,3])
a_set.update({1,2,3},{4,5})
Remember, sets are bags of **unique** values

* set.discard() v.s. set.remove()
remove() will raise KeyError, if value wanted to be deleted is not existed

### Dictionary
* A dictionary is an unordered set of key-value pairs. 


## Comprehension

### List / Dictionary / Set
* You can use any Python expression in a list comprehension, including the functions in the os module for manipulating files and directories.
	* [i**2 for i in range(23)]
	* with os, glob for file manipulations [(os.stat(f).st_size, os.path.realpath(f)) for f in glob.glob('*.xml')]


## Strings
* python 3 supports formatting values into strings. Although this can include very complicated expressions, the most basic usage is to insert a value into a string with single placeholder.

```python
username = "mark"
password = "PapayaWhip"
"{0}'s password is {1}".format(username, password)

"mark's password is PapayaWhip"
```

more complicated one, replacement fields are much more powerful than that. {0} is replaced by the 1st format() argument. {1} is replaced by 2nd

```python
>>> import humansize
>>> si_suffixes = humansize.SUFFIXES[1000]
>>> si_suffixes
['KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB']
>>> '1000{0[0]} = 1{0[1]}'.format(si_suffixes)


'1000KB = 1MB'
```

more tricks, import sys and sys.modules

```python
>>> import humansize
>>> import sys
>>> '1MB = 1000{0.modules[humansize].SUFFIXES[1000][0]}'.format(sys)

'1MB = 1000KB'
```

```python
return '{0:.1f} {1}'.format(size, suffix)
```
**:.1f**: the second half (including and after the colon) defines the format specifier, which further refines how the replaced variable should be formatted.

### Another String Tricks
* string.split() split('&'). split('=', 1)
string.splitlines()

### String vs Bytes

```python
>>> by = b'abcd\x65' ①
>>> by
b'abcde'
>>> type(by) ②
<class 'bytes'>
>>> len(by) ③
5
>>> by += b'\xff' ④
>>> by
b'abcde\xff'
>>> len(by) ⑤
6
>>> by[0] ⑥
97
>>> by[0] = 102 ⑦
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
TypeError: 'bytes' object does not support item assignment
```

A bytes object is immutable; you can not assign individual bytes. If you need to change individual bytes, you can either use string slicing and concatenation operators (which work the same as strings), or you can convert the bytes object into a bytearray object.

### **Regular Expression**
Case studies in dive into python3

* In a regular expression, ^ matches what follows only at the beginning of the string. If this were **not specified**, the pattern **match no matter** where the M were.

* ? makes a pattern more optional

* combined with ^ and $, the sentence 

* **Using the {n,m} syntax** {n,m} matched between n and m occurrences of a pattern
pattern = '^M{0,3}$'

* (A|B|C) match exactly one of A, B or C

### Verbose regular expression


re.search(pattern, example, **re.VERBOSE**) verbose flag should be set

```python 
>>> pattern = '''
^ # beginning of string
M{0,3} # thousands - 0 to 3 Ms
(CM|CD|D?C{0,3}) # hundreds - 900 (CM), 400 (CD), 0-300 (0 to 3 Cs),
# or 500-800 (D, followed by 0 to 3 Cs)
(XC|XL|L?X{0,3}) # tens - 90 (XC), 40 (XL), 0-30 (0 to 3 Xs),
# or 50-80 (L, followed by 0 to 3 Xs)
(IX|IV|V?I{0,3}) # ones - 9 (IX), 4 (IV), 0-3 (0 to 3 Is),
# or 5-8 (V, followed by 0 to 3 Is)
$ # end of string
'''

>>> re.search(pattern, 'M', re.VERBOSE) ①
<_sre.SRE_Match object at 0x008EEB48>
>>> re.search(pattern, 'MCMLXXXIX', re.VERBOSE) ②
<_sre.SRE_Match object at 0x008EEB48>
>>> re.search(pattern, 'MMMDCCCLXXXVIII', re.VERBOSE) ③
<_sre.SRE_Match object at 0x008EEB48>
>>> re.search(pattern, 'M') ④

```

You should now be familiar with the following techniques:
◦ ^ matches the beginning of a string.
◦ $ matches the end of a string.
◦ \b matches a word boundary.
◦ \d matches any numeric digit.
◦ \D matches any non-numeric character.
◦ x? matches an optional x character (in other words, it matches an x zero or one times).
◦ x* matches x zero or more times.
◦ x+ matches x one or more times.
◦ x{n,m} matches an x character at least n times, but not more than m times.
◦ (a|b|c) matches either a or b or c.
◦ (x) in general is a remembered group. You can get the value of what matched by using the groups() method
of the object returned by re.search.
