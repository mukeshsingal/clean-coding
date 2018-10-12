#Functions

* What is it that makes a function easy to read and understand? 
* How can we make a function communicate its intent? 
* What attributes can we give our functions that will allow a casual reader to intuit the kind of program they live inside?

###1. Small
* The first rule of functions is that they should be small. 
* The second rule of functions is that they should be smaller than that.
* Every function in this program was just two, or three, or four lines long.
* **Blocks and Indenting**
    *   This implies that the blocks within `if` statements, `else` statements, `while` statements, and
        so on should be **one line** long. 
    * Probably that line should be a function call. Not only does this keep the enclosing function            small, but it also adds documentary value because the function called within the block can            have a nicely descriptive name.
    * This also implies that functions **should not** be large enough to hold nested structures.
        Therefore, the indent level of a function should not be greater than one or two. This, of
        course, makes the functions easier to read and understand.

###2. Do One Thing
* **Functions should do one thing.**
* **They should do it well.** 
* **They should do it only.**
* So, another way to know that a function is doing more than “one thing” is if you can
  extract another function from it with a name that is not merely a restatement of its implementation

###3. One Level of Abstraction(Function level) per Function

* In order to make sure our functions are doing `one thing`, we need to make sure that the
statements within our function are all at the same level of abstraction.
* We should not have high, mid and low level abstraction within same function.
* **Reading Code from Top to Bottom: The Stepdown Rule**
    * we want to be able to read from top to bottom of program as though it were a set
      of TO paragraphs, each of which is describing the current level of abstraction and referencing
      subsequent TO paragraphs at the next level down. 
      
###4. Switch Statements
It’s hard to make a small switch statement. Even a switch statement with only two cases is larger than I’d like a single block or function to be. It’s also hard to make a switch statement that does one thing. By their nature, switch statements always do N things. Unfortunately we can’t always avoid switch statements, but we can make sure that each switch statement is buried in a low-level class and is never repeated. We do this, of course, with polymorphism.
 
     ```java
        public Money calculatePay(Employee e) throws InvalidEmployeeType {
            switch (e.type) {
                case COMMISSIONED:
                    return calculateCommissionedPay(e);
                case HOURLY:
                    return calculateHourlyPay(e);
                case SALARIED:
                    return calculateSalariedPay(e);
                default:
                    throw new InvalidEmployeeType(e.type);
            }
        }
    ```
 Problem with the code: 
 1. First, it’s large, and when new
 employee types are added, it will grow. 
 2. Second, it very clearly does more than one thing.
 3. Third, it violates the Single Responsibility Principle because there is more than one
 reason for it to change. 
 4. Fourth, it violates the Open Closed Principle8 (OCP) because it must change whenever new types are added. 
 5. But possibly the worst problem with this function is that there are an unlimited number of other functions that will have the same structure.

The solution to this problem is to bury the switch statement in the basement of an ABSTRACT FACTORY and never let anyone see it. **My general rule for switch statements is that they can be tolerated if they appear only once**, are used to create polymorphic objects, and are hidden behind an inheritance relationship so that the rest of the system can’t see them.

###5. Use Descriptive Names:
_“You know you are working on clean codewhen each routine turns out to be pretty much what you expected.”_

Don’t be afraid to make a name long. A long descriptive name is better than a short
enigmatic name. A long descriptive name is better than a long descriptive comment. Use
a naming convention that allows multiple words to be easily read in the function names,
and then make use of those multiple words to give the function a name that says what
it does.

Don’t be afraid to make a name long. A long descriptive name is better than a short enigmatic name. A long descriptive name is better than a long descriptive comment. Use a naming convention that allows multiple words to be easily read in the function names, and then make use of those multiple words to give the function a name that says what it does.

