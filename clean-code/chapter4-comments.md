# Comments
The proper use of comments is to compensate for our failure to express ourself in code. Note that I used the word failure. I meant it. Comments are always failures. We must have them because we cannot always figure out how to express ourselves without them, but their use is not a cause for celebration.

So when you find yourself in a position where you need to write a comment, think it through and see whether there isn’t some way to turn the tables and express yourself in code. Every time you express yourself in code, you should pat yourself on the back. Every time you write a comment, you should grimace and feel the failure of your ability of expression.

Truth can only be found in one place: the code. Only the code can truly tell you what it does. It is the only source of truly accurate information. Therefore, though comments are sometimes necessary, we will expend significant energy to minimize them.

### 1. Comments Do Not Make Up for Bad Code
One of the more common motivations for writing comments is bad code. We write a module
and we know it is confusing and disorganized. We know it’s a mess. So we say to ourselves, "Ooh, I’d better comment that!" No! You’d better clean it!
Clear and expressive code with few comments is far superior to cluttered and complex
code with lots of comments. Rather than spend your time writing the comments that
explain the mess you’ve made, spend it cleaning that mess.

### 2. Explain Yourself in Code
There are certainly times when code makes a poor vehicle for explanation. Unfortunately,
many programmers have taken this to mean that code is seldom, if ever, a good means for
explanation. This is patently false. Which would you rather see? This:
```
// Check to see if the employee is eligible for full benefits
if ((employee.flags & HOURLY_FLAG) && (employee.age > 65))

Or this?

if (employee.isEligibleForFullBenefits())
```
It takes only a few seconds of thought to explain most of your intent in code. In many
cases it’s simply a matter of creating a function that says the same thing as the comment you want to write. 

### 3. Good Comments
1. Legal Comments

    Sometimes our corporate coding standards force us to write certain comments for legal
    reasons. For example, copyright and authorship statements are necessary and reasonable
    things to put into a comment at the start of each source file.
    Here, for example, is the standard comment header that we put at the beginning of
    every source file in FitNesse. I am happy to say that our IDE hides this comment from acting
    as clutter by automatically collapsing it.

    ```
    // Copyright (C) 2003,2004,2005 by Object Mentor, Inc. All rights reserved.
    // Released under the terms of the GNU General Public License version 2 or later.
    ```

2. Informative Comments

    It is sometimes useful to provide basic information with a comment. For example, consider
    this comment that explains the return value of an abstract method:
    ```
    // Returns an instance of the Responder being tested.
    protected abstract Responder responderInstance();
    ```
    
    A comment like this can sometimes be useful, but it is better to use the name of the function
    to convey the information where possible. For example, in this case the comment
    could be made redundant by renaming the function: **responderBeingTested**.
    
    Here’s a case that’s a bit better:
    ```
    // format matched kk:mm:ss EEE, MMM dd, yyyy
    Pattern timeMatcher = Pattern.compile(
    "\\d*:\\d*:\\d* \\w*, \\w* \\d*, \\d*");
    ```
    In this case the comment lets us know that the regular expression is intended to match a
    time and date that were formatted with the SimpleDateFormat.format function using the
    specified format string. Still, it might have been better, and clearer, if this code had been
    moved to a special class that converted the formats of dates and times. Then the comment
    would likely have been superfluous.
    
3. Explanation of Intent
   
   Sometimes a comment goes beyond just useful information about the implementation and
   provides the intent behind a decision.
   
4. Clarification
   
   Sometimes it is just helpful to translate the meaning of some obscure argument or return
   value into something that’s readable. In general it is better to find a way to make that argument or return value clear in its own right; but when its part of the standard library, or in code that you cannot alter, then a helpful clarifying comment can be useful.
   
   ```java_holder_method_tree
   public void testCompareTo() throws Exception
   {
       WikiPagePath a = PathParser.parse("PageA");
       WikiPagePath ab = PathParser.parse("PageA.PageB");
       WikiPagePath b = PathParser.parse("PageB");
       WikiPagePath aa = PathParser.parse("PageA.PageA");
       WikiPagePath bb = PathParser.parse("PageB.PageB");
       WikiPagePath ba = PathParser.parse("PageB.PageA");
       assertTrue(a.compareTo(a) == 0); // a == a
       assertTrue(a.compareTo(b) != 0); // a != b
       assertTrue(ab.compareTo(ab) == 0); // ab == ab
       assertTrue(a.compareTo(b) == -1); // a < b
       assertTrue(aa.compareTo(ab) == -1); // aa < ab
       assertTrue(ba.compareTo(bb) == -1); // ba < bb
       assertTrue(b.compareTo(a) == 1); // b > a
       assertTrue(ab.compareTo(aa) == 1); // ab > aa
       assertTrue(bb.compareTo(ba) == 1); // bb > ba
   }
   ```
   
   There is a substantial risk, of course, that a clarifying comment is incorrect. Go
   through the previous example and see how difficult it is to verify that they are correct. This
   explains both why the clarification is necessary and why it’s risky. So before writing   comments like this, take care that there is no better way, and then take even more care that they
   are accurate.

5. Warning of Consequences
   
   Sometimes it is useful to warn other programmers about certain consequences. For
   example, here is a comment that explains why a particular test case is turned off:
   
6. TODO Comments
   
   It is sometimes reasonable to leave “To do” notes in the form of //TODO comments. In the
   following case, the TODO comment explains why the function has a degenerate implementation
   and what that function’s future should be.
   
   ```java_holder_method_tree
   //TODO-MdM these are not needed
   // We expect this to go away when we do the checkout model
   protected VersionInfo makeVersion() throws Exception
   {
        return null;
   }   
   ```
   
7. Amplification
   A comment may be used to amplify the importance of something that may otherwise seem inconsequential.
   ```
   String listItemContent = match.group(3).trim();
   // the trim is real important. It removes the starting
   // spaces that could cause the item to be recognized
   // as another list.
   ```

8. Javadocs in Public APIs
   
   There is nothing quite so helpful and satisfying as a well-described public API. The javadocs
   for the standard Java library are a case in point. It would be difficult, at best, to write
   Java programs without them.
   
   If you are writing a public API, then you should certainly write good javadocs for it.
   But keep in mind the rest of the advice in this chapter. Javadocs can be just as misleading,
   nonlocal, and dishonest as any other kind of comment.