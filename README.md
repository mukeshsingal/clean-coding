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
          
   6. Avoid Encodings
   7. Avoid Mental Mapping
   8. Don’t Be Cute
   9. Pick One Word per Concept
   10. Don’t Pun
   11. Use Solution Domain Names
   12. Use Problem Domain Names
   13. Add Meaningful Context
   14. Don’t Add Gratuitous Context
   15. Final Words
   
