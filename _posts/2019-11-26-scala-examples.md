---
layout: post
title:  "Scala Examples"
date:   2019-11-26 13:30:00 +0800
categories: scala
---

### Values, Variables, Types

``` scala
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
``` scala
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
``` scala
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
``` scala
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