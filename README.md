# Clean Code
* You weapon while reviewing any Pull Request.
* These concepts which deserve the space in your cache. 


Chapter 2: Meaningful names

Names are everywhere in software. We name our variables, our functions, our arguments,
classes, and packages. We name our source files and the directories that contain them. We
name our jar files and war files and ear files. We name and name and name. Because we do so much of it, we’d better do it well.


   1. Use Intention-Revealing Names
        * Names should reveal its intent
        * The name of a variable, function, or class, should answer all the big questions. It
          should tell you why it exists, what it does, and how it is used.
        * The name d reveals nothing. It does not evoke a sense of elapsed time, nor of days.            We should choose a name that specifies what is being measured and the unit of that             measurement:
            ```
            int d; // elapsed time in days
            
            int elapsedTimeInDays;
            int daysSinceCreation;
            int daysSinceModification;
            int fileAgeInDays;
            ```
   2. Avoid Disinformation
        * Programmers must avoid leaving false clues that obscure the meaning of code. 
        Do not refer to a grouping of accounts as an accountList unless it’s actually a List. 
        If the container holding the accounts is not actually a List, it may lead to false conclusions. 
   3. Make Meaningful Distinctions
        * Programmers create problems for themselves when they write code solely to satisfy a compiler or interpreter.
        * Number-series naming (a1, a2, .. aN) is the opposite of intentional naming. Such
        names are not dis-informative - they are non-informative; they provide no clue to the
        author’s intention. Consider:
            ```
            public static void copyChars(char a1[], char a2[]) {
                for (int i = 0; i < a1.length; i++) {
                a2[i] = a1[i];
                }
            }
            ```
            This function reads much better when source and destination are used for the argument
            names.
        * Noise words are another meaningless distinction. Imagine that you have a Product
         class. If you have another called ProductInfo or ProductData, you have made the names different
         without making them mean anything different. Info and Data are indistinct noise
         words like a, an, and the.
         * In the absence of specific conventions, the variable moneyAmount is indistinguishable
         from money, customerInfo is indistinguishable from customer, accountData is indistinguishable
         from account, and theMessage is indistinguishable from message. Distinguish names in
         such a way that the reader knows what the differences offer.
   4. Use Pronounceable Name
        * Names should be pronounceable otherwise it will be really hard to discuss or describe the code.
        * Look at below examples
         ```java
            class DtaRcrd102 {
                private Date genymdhms;
                private Date modymdhms;
                private final String pszqint = "102";
                /* ... */
            }
            //To
            class Customer {
                private Date generationTimestamp;
                private Date modificationTimestamp;
                private final String recordId = "102";
                /* ... */
            }
            ```  
   5. Use Searchable Names
        * Single-letter names and numeric constants have a particular problem in that they are not
          easy to locate across a body of text. One might easily grep for MAX_CLASSES_PER_STUDENT.              Likewise, the name e is a poor choice for any variable for which a programmer might need to           search.
        *  My personal preference is that single-letter names can ONLY be used as local variables
           inside short methods.
             
   6. Avoid Mental Mapping
        * Readers shouldn’t have to mentally translate your names into other names they already
          know. This problem generally arises from a choice to use neither problem domain terms
          nor solution domain terms.   
        * One difference between a smart programmer and a professional programmer is that
          the professional understands that clarity is king. Professionals use their powers for good
          and write code that others can understand.
        * Classes and objects should have noun or noun phrase names like Customer, WikiPage,
          Account, and AddressParser. Avoid words like Manager, Processor, Data, or Info in the name
          of a class. A class name should not be a verb.
        * Methods should have verb or verb phrase names like postPayment, deletePage, or save.
          Accessors, mutators, and predicates should be named for their value and prefixed with get,
          set, and is according to the javabean standard.
          
          ```
          string name = employee.getName();
          customer.setName("mike");
          if (paycheck.isPosted())...
          ```
          
          When constructors are overloaded, use static factory methods with names that
          describe the arguments. For example,
          
          `Complex fulcrumPoint = Complex.FromRealNumber(23.0);`
          
          is generally better than
          
          `Complex fulcrumPoint = new Complex(23.0);`
          
          Consider enforcing their use by making the corresponding constructors private.
   8. Don’t Be Cute
        * If names are too clever, they will be memorable only to people who share the
        author’s sense of humor, and only as long as these people remember the joke. Will
        they know what the function named `HolyHandGrenade` is supposed to do? Sure,
        it’s cute, but maybe in this case `DeleteItem`s might be a better name.
        Choose **clarity** over **entertainment** value.
   9. Pick One Word per Concept
        * It’s confusing to have a controller and a manager and a driver in the same
          code base. What is the essential difference between a DeviceManager and a Protocol-
          Controller? Why are both not controllers or both not managers? Are they both Drivers
          really? The name leads you to expect two objects that have very different type as well as
          having different classes.
          A consistent lexicon is a great boon to the programmers who must use your code.
   10. Don’t Pun
        * Avoid using the same word for two purposes. Using the same term for two different ideas is essentially a pun.
        * If you follow the **one word per concept** rule, you could end up with many classes that have, for example, an 
        add method. As long as the parameter lists and return values of the various add methods are semantically 
        equivalent, all is well. However one might decide to use the word add for **consistency** when he or she is not
        in fact adding in the same sense. Let’s say we have many classes where add will create a new value by adding 
        or concatenating two existing values. Now let’s say we are writing a new class that has a method that puts its 
        single parameter into a collection. Should we call this method add? It might seem consistent because we have 
        so many other add methods, but in this case, the semantics are different, so we should use a name like insert 
        or append instead. To call the new method add would be a pun.
   11. Use Solution Domain Names
        * Remember that the people who read your code will be programmers. So go ahead and use computer science (CS) terms, 
        algorithm names, pattern names, math terms, and so forth. It is not wise to draw every name from the problem domain 
        because we don’t want our coworkers to have to run back and forth to the customer asking what every name means when 
        they already know the concept by a different name. The name AccountVisitor means a great deal to a programmer who is 
        familiar with the VISITOR pattern. What programmer would not know what a JobQueue was? There are lots of very 
        technical things that programmers have to do. Choosing technical names for those things is usually the 
        most appropriate course.
   12. Use Problem Domain Names
        * Separating solution and problem domain concepts is part of the job of a good programmer and designer. 
        The code that has more to do with problem domain concepts should have names drawn from the problem domain.
   13. Add Meaningful Context
        * Imagine that you have variables named firstName, lastName, street, houseNumber, city,
          state, and zipcode. Taken together it’s pretty clear that they form an address. But what if
          you just saw the state variable being used alone in a method? Would you automatically
          infer that it was part of an address?
          You can add context by using prefixes: addrFirstName, addrLastName, addrState, and so
          on. At least readers will understand that these variables are part of a larger structure. Of
          course, a better solution is to create a class named Address. Then, even the compiler knows
          that the variables belong to a bigger concept.
   14. Don’t Add Gratuitous Context
        * In an imaginary application called “Gas Station Deluxe,” it is a bad idea to prefix every
          class with GSD. Frankly, you are working against your tools. You type G and press the completion
          key and are rewarded with a mile-long list of every class in the system. Is that
          wise? Why make it hard for the IDE to help you?
          Likewise, say you invented a MailingAddress class in GSD’s accounting module, and
          you named it GSDAccountAddress. Later, you need a mailing address for your customer contact
          application. Do you use GSDAccountAddress? Does it sound like the right name? Ten of
          17 characters are redundant or irrelevant.   
   
   
