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




