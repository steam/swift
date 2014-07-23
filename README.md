#Swift Outline


##Expressions
Using the Swift REPL (Read Eval Print Loop)

`1+1`















##Variables

`var name = "Sean"`

same as 

`var name: String = "Sean"`














##Type Inference

`name = 666` // fails because `name` is a String












##Constants

`let age = 35`

`age = 36` // cannot change the value of a constant













##Strings

`var fullName = name + " " + "Dougherty"`














##Arrays

`var names = ["Sean", "Carrie"]`

appending items and other arrays

`names += "Jack"`

`names += ["Cael", "Liam"]` 

`names[1]`

slicing arrays

`var kids = names[2...4]`

`names += 123` // cannot add `Int` to a `String` array

specifying type

`var ages:[Int] = [1, 2, 3]`















##Dictionaries

`var family = ["Sean" : 35, "Carrie" : 36, "Jack" : 9, "Cael" : 7, "Liam" : 3]`

`family["Cael"]`










### ---> Switch to Guard <---











## Optionals

Optionals have a value or no value at all

`var age: Int?`

Cannot access directly

`age + 4` // unsafe, won't compile

unwrap with `!`

`age! + 4` // allowed but causes crash becase age has no value

1. checking for value using if let syntax

```
if let bobAge = family["Bob"] {
  println("Bob is \(bobAge) years old") // doesn't get called
}
```

```
if let liamAge = family["Liam"] {
  println("Liam is \(liamAge) years old")
}
```


## Optional Chaining

```
if let roomCount = john.residence?.numberOfRooms {
    println("John's residence has \(roomCount) room(s).")
} else {
    println("Unable to retrieve the number of rooms.")
}
```








##Looping
*Strings

`var company = "Modeset"`

```
for letter in company {
	println("The letter is \(letter)")
}
```

*Arrays

`let animals = ["Cat", "Dog", "Horse"]`

```
for animal in animals {
	println("The animal is \(animal)")
}
```

*Dictionaries

`var family = ["Sean" : 35, "Carrie" : 36, "Jack" : 9, "Cael" : 7, "Liam" : 3]`

```
for (name, age) in family {
	println("\(name) is \(age) years old")
}
```





##if statements

`let hasValue = true`

```
if hasValue {
	println("It has a value")
}
```


##switch statements
1.Pattern Matching


`let yetAnotherPoint = (1, -1)`

```
switch yetAnotherPoint {
case let (x, y) where x == y:
    println("(\(x), \(y)) are the same")
case let (x, y) where x == -y:
    println("(\(x), \(y)) x is equal to the negative of y")
case let (x, y):
    println("(\(x), \(y)) x and y are arbitrary")
}
```

`let vegetable = "red pepper"`

```
switch vegetable {
case "celery":
  println("Add some raisins and make ants on a log.")
case "cucumber", "watercress":
  println("That would make a good tea sandwich.")
case let x where x.hasSuffix("pepper"):
  println("Is it a spicy \(x)?")
default:
  println("Everything tastes good in soup.")
}
```


##Tuples

```
let error = (404, "Not Found")

let (statusCode, statusMessage) = error

println(statusCode)
println(statusMessage)
```


##Functions

```
func isError(statusCode:Int) -> Bool {
	return statusCode >= 400 && statusCode < 500
}

println(isError(statusCode))
```






##Classes, Protocols, Structs

1. Create class animal and makeSound method

2. add concrete Dog class and override makeSound method

3. create a Dog

4. create global function "play()"

5. Add let 'name' to Animal 

6. add var 'energy' to animal, set to 100

7. decrement energy by 5 in Animal makeSound, println

8. call super.makeSound() in Dog makeSound method

9. call play several times on dog

10. define 'eat()' function on Animal, receives an edible

11. move printLn of energy into a printEnergy() function

12. define Edible protocol

13. define Banana stuct that conforms to Edible

14. have dog instance eat a Banana()

15. define Molly class that extends Dog

16. override the eat func on Molly and guard against eating bananas

17. Molly().eat(Banana())

18. Create a DogTreat that conforms to Edibile

19. Molly().eat(DogTreat())


```
class Animal {
  let name: String
  var energy = 100

  init(name: String) {
    self.name = name
  }

  func makeSound() {
    energy -= 5
    printEnergy()
  }

  func eat(food: Edible) {
    println("[\(name) is eating a \(food.name) for \(food.value) energy]")
    energy += food.value
    printEnergy()
  }

  func printEnergy() {
    println("[\(name) now has \(energy) energy]")
  }
}
```

```
class Dog: Animal {
  override func makeSound() {
    println("Bark")
    super.makeSound()
  }
}
```

```
class Molly: Dog {
  init() {
    super.init(name: "Molly")
  }

  override func eat(food: Edible) {
    if food as? Banana {
      println("YUCK")
    } else {
      super.eat(food)
    }
  }
}
```

```
protocol Edible {
  var name: String { get }
  var value: Int { get }
}
```


```
struct Banana: Edible {
  var name: String { get { return "Banana" } }
  var value: Int { get { return 10 } }
}
```
```
struct DogTreat: Edible {
  var name: String { get { return "Dog Treat" } }
  var value: Int { get { return 5 } }
}
```


```
func play(animal: Animal) {
  println("Playing with \(animal.name)")
  animal.makeSound()
}

let dog = Dog(name: "Fido")
play(dog)
play(dog)
play(dog)
play(dog)

dog.eat(Banana())

Molly().eat(Banana())
Molly().eat(DogTreat())
```





##Closures

```
func introToFriends(friendOne:String, friendTwo:String) -> String {
	return "\(friendOne) I'd like you to meet \(friendTwo)"
}

let output = introToFriends("jon", "mike")

println(output)
```

```
var closure:() -> () {
	
}
```

`var combine:(String,String) -> String`

```
combine = {
	a,b -> String in
	return a + b
}
```

```
combine = {
	a,b -> String in a + b
}
```

`combine("Hello", "world!")`


`combine = { $0 + $1}`






## ---> Switch to Playground <---





##Generics
Write flexible, reusable functions and types that can work with any type.
Most of Swift's entire library is built on generics. Type inference is replaced with place holders.


```
struct IntStack {
	var items = [Int]()

	mutating func push(item:Int) {
		items.append(item)
	}

	mutating func pop() -> Int {
		return items.removeLast()
	}
}
```

```
var intStack = IntStack()
intStack.push(1)
intStack.push(2)
intStack.push(3)
intStack.pop()
intStack
```

```
struct Stack<T> {
	var items = [T]()

	mutating func push(item:T) {
		items.append(item)
	}

	mutating func pop() -> T {
		return items.removeLast()
	}
}
```

```
var stringStack = Stack<String>()
stringStack.push("Matt")
stringStack.push("Jeremy")
stringStack.push("Ken")
stringStack.pop()
stringStack
```
