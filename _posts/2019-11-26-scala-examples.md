---
layout: post
title:  "Scala Examples"
date:   2019-11-26 13:30:00 +0800
categories: scala
---

### Values, Variables, Types

```scala
object ValuesVariablesTypes extends App {
  val x: Int = 42
  println(x)

  // VALS are immutable
  // COMPILER can infer types

  val aString: String = "hello"
  val anotherString = "goodbye"
  val aBoolean: Boolean = false
  val aChar: Char = 'a'
  val anInt: Int = x
  val aShort: Short = 12345
  // add L at the end to tell the compiler that it is a long literal
  val aLong: Long = 12345678910L
  // add F at the end to tell the compiler that it is a float literal
  val aFloat: Float = 2.0F

  // variables
  var aVariable: Int = 4

  // variables can be reassign
  aVariable = 5 // side effects
}
```

### Expressions
```scala
object Expressions extends App {

  val x = 1 + 2 // EXPRESSION
  println(x)

  println(2 + 3 * 4)
  // + - * / & | ^ << >> >>> (right shift with zero extension)

  println(1 == x)
  // == != > >= < <=

  println(!(1 == x))
  // ! && ||

  var aVariable = 2
  aVariable += 3 // -= *= /=
  println(aVariable)

  // Instructions (DO) vs Expressions (VALUE)

  // IF expression
  val aCondition = true
  val aConditionedValue = if (aCondition) 5 else 3
  println(aConditionedValue)
  println(if(aCondition) 5 else 3)
  println(1 + 3)

  var i = 0
  while (i < 10) {
    println(i)
    i += 1
  }

  // NEVER WRITE THIS AGAIN
  // EVERYTHING in Scala is an Expression!

  val aWeirdValue = (aVariable = 3) // Unit === void
  println(aWeirdValue)

  // side effects: println(), whiles, reassigning

  // Code blocks (also an expression)
  val aCodeBlock = {
    val y = 2
    val z = y + 1

    if (z > 2) "hello" else "goodbye"
  }

  // 1. difference between "hello world" vs println("hello world")?
  // 2. What are the values?

  val someValue = {
    2 < 3
  }

  val someOtherValue = {
    if (someValue) 239 else 986
    42
  }
}
```

### Functions
```scala
object Functions extends App {

  def aFunction(a: String, b: Int) = {
    a + " " + b
  }

  println(aFunction("Hello", 3))

  def aParameterlessFunction(): Int = 42

  println(aParameterlessFunction())
  println(aParameterlessFunction)

  // WHEN YOU NEED LOOPS, USER RECURSION.
  // RECURSIVE FUNCTION NEEDS EXPLICIT RETURN TYPE
  def aRepeatedFunction(aString: String, n: Int): String = {
    if (n == 1) aString
    else aString + aRepeatedFunction(aString, n - 1)
  }

  println(aRepeatedFunction("hello", 3))

  def aFunctionWithSideEffects(aString: String): Unit = println(aString)

  def aBigFunction(n: Int): Int = {
    def aSmallerFunction(a: Int, b: Int): Int = a + b

    aSmallerFunction(n, n - 1)
  }

  /*
  1. A greeting function (name, age) => "Hi, my $name is $name and i am $age years old"
  2. Factorial function 1 * 2 * 3 * .. * n
  3. A Fibonacci function
     f(1) = 1
     f(2) = 1
     f(n) = f(n - 1) + f(n - 2)
  4. Tests if a number is prime.
   */

  def greeting(name: String, age: Int): Unit = {
    println(s"Hi, my name is $name and i am $age years old")
  }

  greeting("Joe", 31)

  def factorial(n: Int): Int = {
    if (n == 0) {
      return 1
    }
    System.out.print(n + " ");
    n * factorial(n - 1)
  }

  println(factorial(5))

  def fibonacci(n: Int): Int = {
    if (n <= 2) 1
    else fibonacci(n - 1) + fibonacci(n - 2)
  }

  println(fibonacci(8))

  def isPrime(n: Int): Boolean = {
    def isPrimeUntil(t: Int): Boolean =
      if (t <= 1) true
      else n % t != 0 && isPrimeUntil(t - 1)

    isPrimeUntil(n / 2)
  }

  println(isPrime(37))
  println(isPrime(2003))
  println(isPrime(37 * 17))
}
```

### Pass by value VS Pass by name
```scala
object CBNvsCBV extends App {

  def calledByValue(x: Long): Unit = {
    println("by value: " + x)
    println("by value: " + x)
  }

  def calledByName(x: => Long): Unit = {
    println("by name: " + x)
    println("by name: " + x)
  }

  calledByValue(System.nanoTime())
  calledByName(System.nanoTime())

  def infinite(): Int = 1 + infinite()
  def printFirst(x: Int, y: => Int) = println(x)

  // below code crashes because infinite gets evaluated
  //  printFirst(infinite(), 34)
  printFirst(34, infinite())
}
```

### Default Arguments

```scala
object DefaultArgs extends App {

  def trFact(n: Int, acc: Int = 1): Int =
    if (n <= 1) acc
    else trFact(n - 1, n * acc)

  val fact10 = trFact(10, 2)

  def savePicture(format: String = "jpg", width: Int = 1920, height: Int = 1080): Unit = println("saving picture")
  savePicture(width = 800)

  /*
    1. pass in every leading argument
    2. name the arguments
   */

  savePicture(height = 600, width = 800, format = "bmp")
}
```

### String Interpolators

```scala
object StringOps extends App {

  val str: String = "Hello, I am learning Scala"

  println(str.charAt(2))
  println(str.substring(7, 11))
  println(str.split(" ").toList)
  println(str.startsWith("Hello"))
  println(str.replace(" ", "-"))
  println(str.toLowerCase())
  println(str.length())

  // scala
  val aNumberString = "45"
  val aNumber = aNumberString.toInt
  println('a' +: aNumberString :+ 'z')
  println(str.reverse)
  println(str.take(2))

  // Scala-specific String interpolation
  val name = "David"
  val age = 12
  val greeting = s"Hello, my name is $name and I am $age years old."
  val anotherGreeting = s"Hello, my name is $name and I will be turning ${age + 1} years old."

  println(greeting)
  println(anotherGreeting)

  // F-interpolators
  val speed = 1.2f
  val myth = f"$name%s can eat $speed%2.2f burgers per minute"
  println(myth)

  // raw-interpolator
  println(raw"This is a \n newline")
  val escaped = "This is a \n newline"
  println(escaped)
}
```

### OOP

```scala
object OOBasics extends App {
  val person = new Person("John", 26)
  println(person.age)
  person.greet("abantej")

  val author = new Writer("Charles", "Dickens", 1990)
  val imposter = new Writer("Charles", "Dickens", 1990)
  val novel = new Novel("Great Expectations", 1861, author)

  println(novel.authorAge)
  println(novel.isWrittenBy(author)) // true
  println(novel.isWrittenBy(imposter)) // false

  val counter = new Counter
  counter.inc.print
  counter.dec.print
}

// constructor
class Person(name: String, val age: Int) {
  // body
  val x = 2

  println(1 + 3)

  // method
  def greet(name: String): Unit = println(s"${this.name} says: Hi, $name")

  // overloading
  def greet(): Unit = println(s"Hi, I am $name")

  // multiple constructors
  def this(name: String) = this(name, 0)
}

// class parameters are NOT FIELDS unless you declare them with val or var

/*
  Novel and a Writer

  Writer: first name, surname, year
  - method fullname

  Novel: name, year of release, author
  - authorAge
  - isWrittenBy(author)
  - copy (new year of release) = new instance of Novel
 */

class Writer(firstName: String, surname: String, val year: Int) {
  def fullName: String = firstName + " " + surname
}

class Novel(name: String, year: Int, author: Writer) {
  def authorAge = year - author.year
  def isWrittenBy(author: Writer) = author == this.author
  def copy(newYear: Int): Novel = new Novel(name, newYear, author)
}

/*
  Counter class
  - receives an int value
  - method current count
  - method to increment/decrement => new Counter
  - overload inc/dec to receive an amount
 */

class Counter(val count: Int = 0) {

  def inc: Counter = {
    println("incrementing")
    new Counter(count + 1) // immutability
  }

  def dec: Counter = {
    println("decrementing")
    new Counter(count - 1)
  }

  def inc(n: Int): Counter = {
    if (n <= 0) this
    else inc.inc(n - 1)
  }

  def dec(n: Int): Counter = {
    if (n <= 0) this
    else dec.dec(n - 1)
  }

  def print = println(count)
}
```

### Method Notations

```scala
import scala.language.postfixOps

object MethodNotations extends App {

  class Person (val name: String, favoriteMovie: String) {
    def likes(movie: String): Boolean = movie == favoriteMovie
    def hangOutWith(person: Person): String = s"${this.name} is hanging out with ${person.name}"
    def +(person: Person): String = s"${this.name} is hanging out with ${person.name}"
    def unary_! : String = s"$name, what the heck?!"
    def isAlive: Boolean = true
    def apply(): String = s"Hi, my name is $name and I like $favoriteMovie"
  }

  val mary = new Person("Mary", "Inception")
  println(mary.likes("Inception"))
  println(mary likes "Inception") // equivalent
  // infix notation = operator notation - works on methods with single parameter - an example of syntactic sugar

  // "operators" in scala
  val tom = new Person("Tom", "Fight Club")
  println(mary hangOutWith tom)
  println(mary.+(tom))

  println(1 + 2)
  println(1.+(2))

  // ALL OPERATORS ARE METHODS
  // Akka actors have ! ?

  // prefix notation
  val x = -1 // equivalent to 1.unary_-
  val y = 1.unary_-
  // unary_ prefix only works with - + ~ !

  println(!mary)
  println(mary.unary_!)

  // postfix notation - only available to methods without parameter
  println(mary isAlive)

  // apply
  println(mary.apply())
  println(mary())
}
```