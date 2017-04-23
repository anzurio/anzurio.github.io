## In-code Comments

I have always striven to make my code maintanable by means of making its logical path obvious. I achieve this in big part by giving meaningful names to identifiers and making functions perform one thing only. Given this, I have always thought of in-code comments unnecessary: if my code is readable, understandable, and obvious, wouldn't comments just be redundant?. This not to be confused with public interface documentation which, more often than not, comes in the form of large comment blocks preceding the definition of the unit to be documented. 

In the earliest programming courses of college, I could not help but to roll my eyes every time a professor, after reviewing a given programming assignment, remarked that my program needed documentation even though I had provided that; what they were *really* wanting is for my code to have a few comments within its logical implementation as such, I ended up with needless text such as:

```java
    // Initialize the matrix.
    int[][] matrix = new int[rows][columns];
```

From my perspective, in-line comments should only be used when the code is not obvious but then again, if it is not obvious, probably one should re-think the implementation. The following code resembles something I recently encountered that would have baffled me:

```c#
   if (Compare(currentSubject, updatedSubject) != 0)
   {
       Merge(currentSubject, updatedSubject);    
   }
   //update modified to prevent deletion
   repository.Update(currentSubject.Id, currentSubject);
```

If it were not for that comment I would probably had moved the `repository.Update` call inside the `if` but, as it turns out, somewhere else, the program is relying on the subject repository's individual subject touch information to make a decision whether or not to mark a subject as inactive. Nevertheless, the "need" to have such a comment tells us that code is probably not the most obvious and in fact, the underlying framework might require some serious refactoring.







