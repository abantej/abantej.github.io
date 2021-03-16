---
layout: post
title:  "Scala Basics"
date:   2021-03-14 11:30:00 +0800
categories: scala
---

## String Interpolation
```scala
object RolePlayingGame {
  def main(args: Array[String]): Unit = {
    val playerName = "PlayerOne"
    val role = "wizard"
    println("My name is " + playerName + " and my role is " + role)
    // string interpolation
    println(s"My name is $playerName and my role is $role")
    // f string interpolation
    println(f"My name is $playerName%s and my role is $role%s")
    // raw string interpolation
    println(raw"Hello \nworld")
  }
}
```
```
My name is PlayerOne and my role is wizard
My name is PlayerOne and my role is wizard
My name is PlayerOne and my role is wizard
Hello \nworld
```

## IF ELSE Statement
```scala
object RolePlayingGame {
  def main(args: Array[String]): Unit = {
    val level = 40
    val jobLevel = 40
    var result = ""

    if (level == 40) {
      result = "level is 40"
    } else {
      result = "level is not 40"
    }

    println(result)

    val result2 = if (level == 30) "level is 30" else "level is not 30"
    println(result2)

    println(
    if (level == 20) 
      "level is 20" 
    else 
      "level is not 20")

    println(
      if (level == 40 && jobLevel == 40) 
        "level and jobLevel is the same" 
      else 
        "level and jobLevel is not the same")

  }
}
```
```
level is 40
level is not 30
level is not 20
level and jobLevel is the same
```

## While Loops
```scala
object RolePlayingGame {
  def main(args: Array[String]): Unit = {
    var HP = 100;
    val damage = 20;

    while (HP > 0) {
      HP -= damage
      println(s"Your character took $damage damage. Your HP is now $HP.")
    }

    HP = 100

    println(s"You drank a potion. Your HP is now $HP")

    do {
      HP -= damage
      println(s"Your character is taking damage again. Your HP is now $HP.")
    } while (HP > 0)
  }
}
```
```scala
Your character took 20 damage. Your HP is now 80.
Your character took 20 damage. Your HP is now 60.
Your character took 20 damage. Your HP is now 40.
Your character took 20 damage. Your HP is now 20.
Your character took 20 damage. Your HP is now 0.
You drank a potion. Your HP is now 100
Your character is taking damage again. Your HP is now 80.
Your character is taking damage again. Your HP is now 60.
Your character is taking damage again. Your HP is now 40.
Your character is taking damage again. Your HP is now 20.
Your character is taking damage again. Your HP is now 0.
```

## For Loops
```scala
object RolePlayingGame {
  def main(args: Array[String]): Unit = {
    for (i <- 1 to 3) {
      println(s"You are attacking, repeatedly!")
    }
    for (i <- 1.to(3)) {
      println(s"You are attacking again, repeatedly!")
    }
    for (i <- 1 until 3) {
      println(s"You are attacking once again, repeatedly!")
    }
    for (i <- 1.until(3)) {
      println(s"You are attacking once more, repeatedly!")
    }
    for (i <- 1 to 2; j <- 1 to 3) {
      println("i using multiple ranges " + i + " " + j)
    }

    val list = List(1,2,9,4,10)
    for (i <- list) {
      println("i using lst " + i)
    }

    for (i <- list; if i < 6) {
      println("i using filters " + i)
    }

    val result = for {i <- list; if i < 6} yield {
      i * i
    }
    println(s"result = $result")
  }
}
```
```
You are attacking, repeatedly!
You are attacking, repeatedly!
You are attacking, repeatedly!
You are attacking again, repeatedly!
You are attacking again, repeatedly!
You are attacking again, repeatedly!
You are attacking once again, repeatedly!
You are attacking once again, repeatedly!
You are attacking once more, repeatedly!
You are attacking once more, repeatedly!
i using multiple ranges 1 1
i using multiple ranges 1 2
i using multiple ranges 1 3
i using multiple ranges 2 1
i using multiple ranges 2 2
i using multiple ranges 2 3
i using lst 1
i using lst 2
i using lst 9
i using lst 4
i using lst 10
i using filters 1
i using filters 2
i using filters 4
result = List(1, 4, 16)
```

## Match Expressions
```scala
object RolePlayingGame {
  def main(args: Array[String]): Unit = {
    val heroLevel = 50
    val heroClass = "Swordsman"

    heroLevel match {
      case 20 => println(s"Your level is $heroLevel")
      case 35 => println(s"Your level is $heroLevel")
      case 50 => println(s"Your level is $heroLevel")
      case _ => println("Your level cannot be determined")
    }

    val result = heroClass match {
      case "Swordsman" => "Swordsman"
      case "Wizard" => "Wizard"
      case "Priest" => "Priest"
      case _ => "Your class cannot be determined."
    }
    println(s"Your hero class is $result")

    heroClass match {
      case "Swordsman" | "Assassin" | "Barbarian" => 
        println("Your class is a physical type")
      case "Magician" | "Warlock" | "Force Blader" => 
        println("Your class is a magical type")
    }
  }
}
```
```scala
Your level is 50
Your hero class is Swordsman
Your class is a physical type
```

## Scala Functions
```scala
object RolePlayingGame {
  object Skill {
    def vermillion(chant: String = "Chanting.."): Unit = {
      println(chant)
    }
  }
  def addTotalDamage(total: Int, damage: Int): Int = {
    total + damage
  }

  def levelUpSkill(level: Int): Unit = println(s"Level up skill by $level")

  def main(args: Array[String]): Unit = {
    var currentDamage = 7080
    currentDamage = addTotalDamage(currentDamage, 20)
    println(s"Your total damage is $currentDamage")
    levelUpSkill(2)
    Skill vermillion "Chanting vermillion spell..."
    Skill.vermillion()
    val add = (x: Int, y: Int) => x + y
    println(add(300, 500))
  }
}
```
```
Your total damage is 7100
Level up skill by 2
Chanting vermillion spell...
Chanting..
800
```

## Higher Order Functions
```scala
object RolePlayingGame {
  def averageHeroLevel(hero1: Int,
           hero2: Int,
           hero3: Int,
           f: (Int, Int) => Int):
  Double = f(f(hero1, hero2), hero3);

  def main(args: Array[String]): Unit = {
    val result = averageHeroLevel(40, 60, 80, (x, y) => (x + y)/2 )
    println(result)
  }
}
```
```
65.0
```