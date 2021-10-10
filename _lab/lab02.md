---
layout: lab
num: lab02
ready: true
desc: "Class Inheritance"
assigned: 2021-10-10 23:59:59.59-7
due: 2021-10-17 23:59:59.59-7
---

In this lab, we'll utilize some inheritance functionality and define various 2D shapes and its properties. You'll have the opportunity to practice: 

* Defining a base class and creating an inheritance hierarchy
* Defining derived classes and inheriting data from a base class
* Overriding inherited methods from the parent class in the derived classes
* Installing pytest and unit testing your code

**Note: In general, it is always important to work on labs and reading early so you can gain the proper context and utilize our office hours to seek assistance / ask clarifying questions during the week before the deadline if needed!**

It may be a good idea to read up on some tools we'll be using in this lab before you get started, specifically Chapter 1.4.6.2 (Inheritance).

In this lab, we will create a new `Shape2D` base class as well as defining specific classes for a couple of 2D shapes that will inherit from the `Shape2D` class.

In addition to defining classes for various shapes, you should test your code for correctness by unit testing various scenarios using pytest.

# Instructions

You will need to create four files:
* `Shape2D.py` - file containing a class definition containing properties all Shapes could possibly have.
* `Circle.py` - file containing a class definition of a Circle that inherits from the `Shape2D` class.
* `Square.py` - file containing a class definition of a Square that inherits from the `Shape2D` class.
* `testFile.py` - file containing pytest functions testing the `Shape2D`, `Circle`, and `Square` classes.

There will be no starter code for this assignment, but rather the class descriptions and required methods are defined in the specification below.

It's recommended that you organize your lab work in its own directory. This way all files for a lab are located in a single folder. Also, this will be easy to import various files into your code using the `import / from` technique shown in lecture.

## `Shape2D.py` class

The `Shape2D.py` file will contain the definition of what a general 2D Shape is.

We will define this class' attributes as follows:

* `color` - `str` that represents the color of the shape.

You should write a constructor that allows the user to construct a `Shape2D` object by passing in values for all the fields. You may assume calls to the constructor will always contain a `str` representing the 2D Shape's color.

* `__init__(self, color)`

In addition to your constructor, your class definition should also support "setter" and "getter" methods that can update and retrieve the state of the Shape2D objects:

* `setColor(self, color)` - updates the color of the 2D Shape
* `getColor(self)` - returns the color of the 2D Shape

Each 2D Shape object should be able to call a method `getShapeProperties(self)` that you will implement, which returns a `str` with minimal 2D Shape information. Since a 2D Shape can be many things, the following output represents what will happen if we call the `getShapeProperties` method after constructing a `Shape2D` object:

```python
s1 = Shape2D("blue")
print(s1.getShapeProperties())
```

<b> Output:</b>

<tt>
Shape: N/A, Color: blue
</tt>

<b>Note:</b> The `s1.getShapeProperties()` return value in the example above does not contain a newline character (`\n`) at the end.

## Circle.py

The `Circle.py` file will contain the definition of what a 2D Circle will have. Since a Circle **IS-A** 2D Shape, we will inherit the values we defined in the `Shape2D` class. Since this lab focuses on inheritance, it is important that **you only provide the method definitions below** (you will not receive full credit if you implement other methods in the `Circle` class definition, even if Gradescope's tests pass).

Your `Circle` class definition should support the following constructor / methods:

* `__init__(self, color, radius)` - Constructor that calls the parent class' (`Shape2D`) constructor and sets the radius parameter as an attribute to the `Circle` class.
* `getRadius(self)` - method that returns the radius value of the circle
* `setRadius(self, radius)` - method that updates the value for the circle's radius
* `computeArea(self)` - method that returns the area of the circle. You may use the following approximation of pi: **3.14159**
* `computePerimeter(self)` - method that returns the perimeter of the circle. You may use the following approximation of pi: **3.14159**
* `getShapeProperties(self)` - method that overrides the inherited `getShapeProperties` method in the `Shape2D` class, and returns a `str` with the properties of a `Circle`. An example output for this method is as follows:

```python
c1 = Circle("blue", 2.5)
print(c1.getShapeProperties())
```

<b> Output:</b>

<tt>
Shape: CIRCLE, Color: blue, Radius: 2.5, Area: 19.6349375, Perimeter: 15.70795
</tt>

<b>Note:</b> The `c1.getShapeProperties()` return value in the example above does not contain a newline character (`\n`) at the end.

## Square.py

The `Square.py` file will contain the definition of what a 2D Square will have. Since a Square **IS-A** 2D Shape, we will inherit the values we defined in the `Shape2D` class. Since this lab focuses on inheritance, it is important that **you only provide the method definitions below** (you will not receive full credit if you implement other methods in the `Square` class definition, even if Gradescope's tests pass).

Your `Square` class definition should support the following constructor / methods:

* `__init__(self, color, side)` - Constructor that calls the parent class' (`Shape2D`) constructor and sets the side parameter of the square as an attribute to the `Square` class.
* `getSide(self)` - method that returns the side value of the square
* `setSide(self, side)` - method that updates the value for the square's side
* `computeArea(self)` - method that returns the area of the square
* `computePerimeter(self)` - method that returns the perimeter of the square.
* `getShapeProperties(self)` - method that overrides the inherited `getShapeProperties` method in the `Shape2D` class, and returns a `str` with the properties of a `Square`. An example output for this method is as follows:

```python
s1 = Square("blue", 2.5)
print(s1.getShapeProperties())
```

<b> Output:</b>

<tt>
Shape: SQUARE, Color: blue, Side: 2.5, Area: 6.25, Perimeter: 10.0
</tt>

<b>Note:</b> The `s1.getShapeProperties()` return value in the example above does not contain a newline character (`\n`) at the end.

## `testFile.py` pytests

This file will contain unit tests using pytest to test if your functionality is correct. Think of various scenarios and method calls to be certain that the state of your objects and return values are correct (provide enough tests such that all method calls in `Shape2D`, `Circle`, and `Square` are covered). Even though Gradescope will not use this file when running the automated tests, it is important to provide this file with various test cases (testing is important!!). We will manually grade your `testFile.py` to make sure your unit tests cover the methods in `Shape2D`, `Circle`, and `Square`.

Pytest will need to be installed on your computer since it does not come with Python by default. Some links for you to use when installing pytest are:
* Installation Guide: <https://docs.pytest.org/en/stable/getting-started.html>
* Windows Installation Guide (created by previous Learning Assistants): [Python and Pytest Installation Guide for Windows](https://drive.google.com/file/d/1nPCwIA8cBAkiJ-kOKZFjkOskD94jmWYn/view)
* If you run into any difficulties when installing pytest, we will be happy to help you out during our office / lab hours!

## Submission

Once you're done with writing your class definition and tests, Submit your `Shape2D.py`, `Circle.py`, `Square.py`, and `testFile.py` files to the `Lab02` assignment on Gradescope. There will be various unit tests Gradescope will run to ensure your code is working correctly based on the specifications given in this lab.

If the tests don't pass, you may get some error message that may or may not be obvious at this point. Don't worry - if the tests didn't pass, take a minute to think about what may have caused the error. Try to think of your pytests and see if you can write a test to help you debug the error (if you haven't already). If you're still not sure why you're getting the error, feel free to ask your TAs or Learning Assistants.
