#Functions

* What is it that makes a function easy to read and understand? 
* How can we make a function communicate its intent? 
* What attributes can we give our functions that will allow a casual reader to intuit the kind of program they live inside?

### 1. Small
* The first rule of functions is that they should be small. 
* The second rule of functions is that they should be smaller than that.
* Every function in this program was just two, or three, or four lines long.
* **Blocks and Indenting**
    *   This implies that the blocks within `if` statements, `else` statements, `while` statements, and
        so on should be **one line** long. 
    * Probably that line should be a function call. Not only does this keep the enclosing function small, but it also adds documentary value because the function called within     the block can have a nicely descriptive name.
    * This also implies that functions **should not** be large enough to hold nested structures.
        Therefore, the indent level of a function should not be greater than one or two. This, of
        course, makes the functions easier to read and understand.

### 2. Do One Thing
* **Functions should do one thing.**
* **They should do it well.** 
* **They should do it only.**
* So, another way to know that a function is doing more than “one thing” is if you can
  extract another function from it with a name that is not merely a restatement of its implementation

### 3. One Level of Abstraction(Function level) per Function

* In order to make sure our functions are doing `one thing`, we need to make sure that the
statements within our function are all at the same level of abstraction.
* We should not have high, mid and low level abstraction within same function.
* **Reading Code from Top to Bottom: The Stepdown Rule**
    * we want to be able to read from top to bottom of program as though it were a set
      of TO paragraphs, each of which is describing the current level of abstraction and referencing
      subsequent TO paragraphs at the next level down. 
      
### 4. Switch Statements
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

### 5. Use Descriptive Names:
_“You know you are working on clean codewhen each routine turns out to be pretty much what you expected.”_

Don’t be afraid to make a name long. A long descriptive name is better than a short
enigmatic name. A long descriptive name is better than a long descriptive comment. Use
a naming convention that allows multiple words to be easily read in the function names,
and then make use of those multiple words to give the function a name that says what
it does.

Don’t be afraid to make a name long. A long descriptive name is better than a short enigmatic name. A long descriptive name is better than a long descriptive comment. Use a naming convention that allows multiple words to be easily read in the function names, and then make use of those multiple words to give the function a name that says what it does.

### 6. Function Arguments
* The ideal number of arguments for a function is zero (niladic). 
* Next comes one (monadic), followed closely by two (dyadic). 
* Three arguments (triadic) should be avoided where possible. 
* More than three (polyadic) requires very special justification—and then shouldn’t be used anyway.

Arguments are even harder from a testing point of view. Imagine the difficulty of writing all the test cases to ensure that all the various combinations of arguments work properly. If there are no arguments, this is trivial. If there’s one argument, it’s not too hard. With two arguments the problem gets a bit more challenging. With more than two arguments, testing every combination of appropriate values can be daunting.

1. Common Monadic Forms
    There are two very common reasons to pass a single argument into a function. 
    1. You may be asking a question about that argument, as in boolean fileExists("MyFile"). 
    2. you may be operating on that argument, transforming it into something else and returning it. For example, InputStream fileOpen(“MyFile”) transforms a file name String into an InputStream return value. These two uses are what readers expect when they see a function.
   
        You should choose names that make the distinction clear, and always use the two
   forms in a consistent context. (See Command Query Separation below.)
   
   3. A somewhat less common, but still very useful form for a single argument function,
   is an event. In this form there is an input argument but no output argument. The overall program is meant to interpret the function call as an event and use the argument to alter the state of the system, for example, void passwordAttemptFailedNtimes(int attempts). Use this form with care. It should be very clear to the reader that this is an event. Choose names and contexts carefully.
   4. Using an output argument instead of a return value for a transformation is confusing. If a function is going to transform its input argument, the transformation should appear as the return value.
   
2. **Flag arguments are ugly**. Passing a boolean into a function is a truly terrible practice. It immediately complicates the signature of the method, loudly proclaiming that this function does more than one thing. It does one thing if the flag is true and another if the flag is false! We should have split the function into two.

3. **Triads** 

    Functions that take three arguments are significantly harder to understand than     dyads. The issues of ordering, pausing, and ignoring are more than doubled. I   suggest you think very carefully before creating a triad.

4. **Argument Objects**
   
   When a function seems to need more than two or three arguments, it is likely that some of those arguments ought to be wrapped into a class of their own. Consider, for example, the difference between the two following declarations:
   ```
   Circle makeCircle(double x, double y, double radius);
   Circle makeCircle(Point center, double radius);
   ```
   Reducing the number of arguments by creating objects out of them may seem like
   cheating, but it’s not. When groups of variables are passed together, the way x and
   y are in the example above, they are likely part of a concept that deserves a name of its own.

5. **Verbs and Keywords** 
    
    Choosing good names for a function can go a long way toward explaining the intent   of the function and the order and intent of the arguments. In the case of a monad, the function and argument should form a very nice verb/noun pair. For example, write(name) is very evocative. Whatever this “name” thing is, it is being “written.” An even better name might be writeField(name), which tells us that the “name” thing is a “field.”
    
### 7. Have no side effects 
Side effects are lies. Your function promises to do one thing, but it also does other hidden things.
```java
public class UserValidator {
    private Cryptographer cryptographer;
    public boolean checkPassword(String userName, String password) {
        User user = UserGateway.findByName(userName);
        if (user != User.NULL) {
            String codedPhrase = user.getPhraseEncodedByPassword();
            String phrase = cryptographer.decrypt(codedPhrase, password);
            if ("Valid Password".equals(phrase)) {
                Session.initialize();
                return true;
            }
        }
        return false;
    }
}
```

The side effect is the call to Session.initialize(), of course. The checkPassword function, by its name, says that it checks the password. The name does not imply that it initializes the session. So a caller who believes what the name of the function says runs the risk of erasing the existing session data when he or she decides to check the validity of the user.

This side effect creates a temporal coupling. That is, checkPassword can only be
called at certain times (in other words, when it is safe to initialize the session). If it is called out of order, session data may be inadvertently lost. Temporal couplings are confusing, especially when hidden as a side effect. If you must have a temporal coupling, you should make it clear in the name of the function. In this case we might rename the function checkPasswordAndInitializeSession, though that certainly violates “Do one thing.”

* Avoid output Arguments: 
    Arguments are most naturally interpreted as inputs to a function. If you have been programming for more than a few years, I’m sure you’ve done a double-take on an argument that was actually an output rather than an input.
    `public void appendFooter(StringBuffer report) instead use report.appendFooter();`

### 8. Command Query Separation

Functions should either do something or answer something, but not both. Either your
function should change the state of an object, or it should return some information about that object. Doing both often leads to confusion.

### 9. Prefer Exceptions to Returning Error Codes

Returning error codes from command functions is a subtle violation of command query
separation. It promotes commands being used as expressions in the predicates of if statements.
`if (deletePage(page) == E_OK)`
This does not suffer from verb/adjective confusion but does lead to deeply nested structures. When you return an error code, you create the problem that the caller must deal with the error immediately.

1. Extract Try/Catch Blocks
Try/catch blocks are ugly in their own right. They confuse the structure of the code and mix error processing with normal processing. So it is better to extract the bodies of the try and catch blocks out into functions of their own.
    ```
    public void delete(Page page) {
        try {
            deletePageAndAllReferences(page);
        }
        catch (Exception e) {
            logError(e);
        }
    }
    private void deletePageAndAllReferences(Page page) throws Exception {
        deletePage(page);
        registry.deleteReference(page.name);
        configKeys.deleteKey(page.name.makeKey());
    }
    private void logError(Exception e) {
        logger.log(e.getMessage());
    }
    ```
    
2. Error Handling Is One Thing
   
   Functions should do one thing. Error handing is one thing. Thus, a function that handles errors should do nothing else. This implies (as in the example above) that if the keyword try exists in a function, it should be the very first word in the function and that there should be nothing after the catch/finally blocks.
   
### 10. Don’t Repeat Yourself

Look back at Listing 3-1 carefully and you will notice that there is an algorithm that
gets repeated four times, once for each of the SetUp, SuiteSetUp, TearDown, and
SuiteTearDown cases. It’s not easy to spot this duplication because the four instances
are intermixed with other code and aren’t uniformly duplicated. Still, the duplication
is a problem because it bloats the code and will require four-fold modification should the algorithm ever have to change. It is also a four-fold opportunity for an error of omission. 

Duplication may be the root of all evil in software. Many principles and practices have
been created for the purpose of controlling or eliminating it. Consider, for example, that all of Codd’s database normal forms serve to eliminate duplication in data. Consider also how object-oriented programming serves to concentrate code into base classes that would otherwise be redundant. **Structured programming, Aspect Oriented Programming, Component
Oriented Programming**, are all, in part, strategies for eliminating duplication. It
would appear that since the invention of the subroutine, innovations in software development
have been an ongoing attempt to eliminate duplication from our source code.

### 11. How Do You Write Functions Like This?
Writing software is like any other kind of writing. When you write a paper or an article, you get your thoughts down first, then you massage it until it reads well. The first draft might be clumsy and disorganized, so you wordsmith it and restructure it and refine it until it reads the way you want it to read. 

When I write functions, they come out long and complicated. They have lots of indenting and nested loops. They have long argument lists. The names are arbitrary, and there is duplicated code. But I also have a suite of unit tests that cover every one of those clumsy lines of code. 

So then I massage and refine that code, splitting out functions, changing names, eliminating duplication. I shrink the methods and reorder them. Sometimes I break out whole classes, all the while keeping the tests passing. In the end, I wind up with functions that follow the rules I’ve laid down in this chapter. I don’t write them that way to start. I don’t think anyone could.

