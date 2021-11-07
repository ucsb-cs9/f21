---
layout: lab
num: lab06
ready: true
desc: "Sorting Apartments"
assigned: 2021-11-07 23:59:59.59-7
due: 2021-11-14 23:59:59.59-7
---

# Introduction

In this lab, you'll have the opportunity to practice:

* Defining classes in Python
* Overloading the `==`, `<`, and `>` operators in a Python class
* Implementing an **O(n log n)** mergesort on a list of Apartment objects
* Writing functions that ensure the list of Apartment objects are in sorted order
* Testing your functionality with pytest

**Note:** It is important that you start this lab early so you can utilize our office hours to seek assistance / ask clarifying questions during the week before the deadline if needed! 

For this lab, you have been hired as a realtor for an up-and-coming property management company located in Isla Vista. You are tasked with renting out as many apartments as you can. In order to do so, you will write a program that will sort apartment objects in a Python List. This allows you to show off the best apartments to possible tennants. It's been decided that the three most important properties of an Apartment object are its **rent**, **meters from campus**, and **condition**. You have decided to sort Apartments as follows. First, you will organize the Apartment by increasing rent. In the event of a tie (several Apartments have the same rent), the meters from UCSB will be used to determine the Apartment's place in the list. The closer the apartment is to campus, the better. If the rent and the meters from campus are the same, then the Apartment's condition will be used to determine the Apartment's place in the list. An apartment can have either a `"bad"`, `"average"`, or `"excellent"` condition - the better the condition is, the better the apartment. You may assume that apartment objects will have either `"bad"`, `"average"`, or `"excellent"` as their condition when comparing / sorting apartments.

This lab will require you to define an `Apartment` class and define functions in the `lab06.py` file. Note that `labO6.py` *does not contain a class definition*.

# Instructions

You will need to create three files:
* `Apartment.py` - file containing a class definition for an Apartment object
* `lab06.py` - file containing mergesort and other functions defined in the `lab06.py` section of this lab
* `testFile.py` - file containing pytest functions testing the overall correctness of your class definitions

There will be no starter code for this assignment, but rather the class descriptions and required methods / functions are defined in the specification below.

You should organize your lab work in its own directory. This way all files for a lab are located in a single folder. Also, this will be easy to import various files into your code using the `import / from` technique shown in lecture.

# `Apartment.py`

The `Apartment.py` file will contain the definition of an `Apartment` class. We will define the Apartment attributes as follows:

* `rent` - integer that represents the rent of the Apartment
* `metersFromUCSB` - integer that represents the Apartment's distance (in meters) from UCSB
* `condition` - string that represents the condition of the Apartment. This stirng will be one of three values: `"bad"`, `"average"`, or `"excellent"`

You should write a constructor that allows the user to construct an apartment object by passing in values for all of the fields. Your constructor should set the `rent`, and `metersFromUCSB` to `0` by default. Also, the condition attribute should be set to `"N/A"` by default.

* `__init__(self, rent, metersFromUCSB, condition)`

In addition to your constructor, your class definition should also support "getter" methods that can receive the state of the Apartment object:

* `getRent(self)`
* `getMetersFromUCSB(self)`
* `getCondition(self)`

You will implement the method

* `getApartmentDetails(self)`

that returns a `str` with all of the Apartment attributes. The string should contain all attributes in the following EXACT format (**Note: There is no `\n` character at the end of this string**):

```python
a0 = Apartment(1204, 200, "bad")
print(a0.getApartmentDetails())
```

<b>Output</b>
```
(Apartment) Rent: $1204, Distance From UCSB: 200m, Condition: bad
```

* Lastly, your `Apartment` class should overload the `>`,`<`, and `==` operators. This will be used when finding the proper position of an Apartment in the list using the specifications in the **Introduction** section of this lab. In this context for example, the `<` operator will return True for `Apartment1 < Apartment2` if Apartment1 is **better than** Apartment2. We reviewed operator overloading in class and the textbook does discuss overloading Python operators. You can also refer to this reference on overloading various operators as well: [https://www.geeksforgeeks.org/operator-overloading-in-python/](https://www.geeksforgeeks.org/operator-overloading-in-python/)

# `lab06.py`

This file will contain functions that sort a list of Apartment objects, ensures that the list of Apartment objects are in ascending (best-to-worst) order according to the specification, retrives information about the n<sup>th</sup> apartment in the list, and gets the top three apartments from the sorted list. These function defintions as well as their descriptions are provided below. Note that in order for the autograder to correctly check your implementation, your function defintions must match exactly as the given specifications.

* `mergesort(apartmentList)` - Performs a mergesort on the apartmentList passed as input. Sorts the Apartment objects based on the specifications in the **Introduction** section of this lab. **Gradescope will test to ensure that your mergesort implementation's Big-O is O(n log n)**
* `ensureSortedAscending(apartmentList)` - method that returns a boolean value. Returns `True` if the apartmentList is sorted correctly in asending order. Returns `False` otherwise
* `getNthApartment(apartmentList, n)` - method that returns a string detailing the Apartment's rent, meters from UCSB, and condition at index n. **Note that there is no newline (`"\n"`) at the end of the string returned by this method**. Make use of the `getApartmentDetails(self)` method you defined in `Apartment.py`. If the nth apartment does not exist, output `"(Apartment) DNE"` (see **Sample Output 3** below)
* `getTopThreeApartments(apartmentList)` - method that returns a labeled, newline separated string detailing the rent, meters from UCSB, and condition of the **top three best apartments** from the `apartmentList`. Note that there can be fewer that three apartments in your list and there is no newline at the end of the string returned by this method. You may assume that `apartmentList` is non-empty. **HINT: Make use of the getApartmentDetails(self) and mergesort(apartmentList) you defined in `lab06.py`.** 

# Sample Output 1

```python
a0 = Apartment(1200, 200, "average")
a1 = Apartment(1200, 200, "excellent")
a2 = Apartment(1000, 100, "average")
a3 = Apartment(1000, 215, "excellent")
a4 = Apartment(700, 315, "bad")
a5 = Apartment(800, 250, "excellent")

apartmentList = [a0, a1, a2, a3, a4, a5]
length = len(apartmentList)

print("First and last apartment in UNSORTED apartmentList ...")

print(getNthApartment(apartmentList, 0))
print(getNthApartment(apartmentList, length-1))

mergesort(apartmentList)

# The sorted apartment list is now as follows. 
# apartmentList = [a4, a5, a2, a3, a1, a0]

print("First and last apartment in SORTED apartmentList ...")

print(getNthApartment(apartmentList, 0))
print(getNthApartment(apartmentList, length-1))
```

<b> Output: </b>
```
First and last apartment in UNSORTED apartmentList ...
(Apartment) Rent: $1200, Distance From UCSB: 200m, Condition: average
(Apartment) Rent: $800, Distance From UCSB: 250m, Condition: excellent

First and last apartment in SORTED apartmentList ...
(Apartment) Rent: $700, Distance From UCSB: 315m, Condition: bad
(Apartment) Rent: $1200, Distance From UCSB: 200m, Condition: average
```

# Sample Output 2

```python
a0 = Apartment(1200, 200, "average")
a1 = Apartment(1200, 200, "excellent")
a2 = Apartment(1000, 100, "average")
a3 = Apartment(1000, 215, "excellent")
a4 = Apartment(700, 315, "bad")
a5 = Apartment(800, 250, "excellent")

apartmentList = [a0, a1, a2, a3, a4, a5]

# Notice that top three apartments are a4, a5, and a2 in that order
# Make sure you understand why

print(getTopThreeApartments(apartmentList))
```

<b> Output: </b>
```
1st: (Apartment) Rent: $700, Distance From UCSB: 315m, Condition: bad
2nd: (Apartment) Rent: $800, Distance From UCSB: 250m, Condition: excellent
3rd: (Apartment) Rent: $1000, Distance From UCSB: 100m, Condition: average
```

# Sample Output 3

```python
a0 = Apartment(2400, 50, "average")
a1 = Apartment(2200, 50, "excellent")

apartmentList = [a0, a1]

print(getNthApartment(apartmentList, 0))
print(getNthApartment(apartmentList, 10))
```

<b> Output: </b>
```
(Apartment) Rent: $2400, Distance From UCSB: 50m, Condition: average
(Apartment) DNE
```

# A Brief Note on Sorting Apartments

A common question for this lab may be:

*The directions say that a0 < a1 should return True if apartment a0 is a better apartment than a1. Intuitively though, why would the apartment that is lesser (<) be "better than" the other apartment?*

Recall that you are sorting apartments in ascending order. For example, if you sorted runners in a race by the position they finished in you would do something like this:

1 4 3 2 5 —> 1 2 3 4 5

It is clear that 1<2, 2<3 etc. Notice that the 1st place runner finished in a "better" position even though they have a "lesser" position than the others. The same concept applies here to apartments.

## testFile.py pytest

This file should import your `Apartment.py` class and your `lab06.py` function. You should write tests using pytest to test if the functionality is correct. Think of various scenarios and edge cases when testing your code. Write your tests first in order to check the correctness of the `Apartment` and then `lab06.py` methods. Gradescope requires `testFile.py` to be submitted before running any autograded tests. You should write at least one test for each method in each of these classes. This includes the overloaded operators but excludes the getter methods.

## Submission

Once you're done with writing your solution and tests, submit your `Apartment.py`, `testFile.py`, and `lab06.py` files to the `Lab06` assignment on Gradescope. There will be various unit tests Gradescope will run to ensure your code is working correctly based on the specifications given in this lab. There also will be tests to ensure that your mergesort in `lab06.py` runs in **O(n log n)** time. Note that if your autograder seems to be running for a really long time, your mergesort may not be running in O(n log n) time.

If the tests don't pass, you may get some error message that may or may not be obvious at this point. Don't worry - if the tests didn't pass, take a minute to think about what may have caused the error. If your tests didn't pass and you're still not sure why you're getting the error, feel free to ask your TAs or Learning Assistants.

<sup>* Lab06 created by Gautam Mundewadi and adapted / updated by Richert Wang (F21)</sup>