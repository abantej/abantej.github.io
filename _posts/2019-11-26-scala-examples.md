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