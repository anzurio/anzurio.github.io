## In-code Comments

I have always striven to make my code maintanable by means of making its logical path obvious. I achieve this in big part by giving meaningful names to identifiers and making functions perform one thing only. Given this, I have always thought of in-code comments as unnecessary: if my code is readable, understandable, and obvious, wouldn't comments just be redundant?. This not to be confused with public interface documentation which, more often than not, comes in the form of large comment blocks preceding the definition of the unit to be documented. 

In the earliest programming courses of college, it was usual for my professors to tell me that my program needed documentation even though I had provided that in the form of API documentation; what they were *really* wanting is for my code to have a few comments within its logical implementation as such, I ended up with needless text such as:

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

If it were not for that comment I would probably had moved the `repository.Update` call inside the `if` but, as it turns out, somewhere else, the program is relying on the repository's individual subject touch information to make a decision whether or not to mark a subject as inactive. Nevertheless, the "need" to have such a comment tells us that code is probably not the most obvious and in fact, the underlying framework might require some serious refactoring.

It might be pointed out that sometimes we rely on a third party whose source is not available for us to modify and its behaviour is not what we would usually expect. In this scenario, while true that a comment might be required to alert others that there is something unconventional about that function, it is also reasonable–and I would actually recommend–to wrap it around a function of our own in which we document the odd behaviour of the external function. 

Although I don't want to make a case for what is "obvious" code, I would also encourage not to add comments explaining syntax or language features no matter how obscure or complicated these are. For instance:

```c++
/* "identifier" is a constant pointer (cannot point to a different location) 
 * to a constant int (its value cannot be modified).
 */
int const * const identifier = ...;
```

Perhaps, not commenting something like this will encourage both the author and the maintainer to agilize their minds–through repetition–such that even more complicated syntax would come as naturally as `int identifier = ...`.

