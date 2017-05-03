## In-code Comments

I have always striven to make my code maintainable by means of making its logical path obvious. I achieve this in big part by giving meaningful names to identifiers and making functions perform one thing only. Given this, I have always thought of in-code comments as unnecessary: if my code is readable, understandable, and obvious, wouldn't comments just be redundant?. This is not to be confused with public interface documentation which, more often than not, comes in the form of large comment blocks preceding the definition of the unit to be documented.

In the earliest programming courses of college, it was usual for my professors to tell me that my program needed documentation even though I had provided that in the form of API documentation; what they were really wanting is for my code to have a few comments within its logical implementation as such, I ended up with needless text such as:


```java
    // Initialize the matrix.
    int[][] matrix = new int[rows][columns];
```

From my perspective, in-code comments should only be used when the code is not obvious but then again, if it is not obvious, probably one should re-think the implementation. The following code resembles something I recently encountered that would have baffled me:

```c#
   if (Compare(currentSubject, updatedSubject) != 0)
   {
       Merge(currentSubject, updatedSubject);    
   }
   //update modified to prevent deletion
   repository.Update(currentSubject.Id, currentSubject);
```

If it were not for that comment I would probably had moved the repository.Update call inside the if but, as it turns out, somewhere else, the program is relying on the repository's individual subject touch information to make a decision whether or not to mark a subject as inactive. Nevertheless, the "need" to have such a comment tells us that code is probably not the most obvious and in fact, the underlying framework might require some serious refactoring.

On the other hand, a good company-wide culture of the use of small incremental changes towards source control (in `git` lingo: commits) with precise descriptions could also be a great replacement for this sort of in-code comments. In the scenario above, I could have looked at the code and known that, such an odd-feeling choice of statement ordering might have a reason of being and that reason could be found in the file’s change history.

It might be pointed out that sometimes we rely on a third party whose source is not available for us to modify and its behaviour is not what we would usually expect. In this scenario, while true that a comment might be required to alert others that there is something unconventional about that function, it is also reasonable–and I would actually recommend–to wrap it around a function of our own in which we document the odd behaviour of the external function. For instance, let us imagine we are consuming a C# third party Complex Number definition which contains a `TryParse` method, however, this method's signature is different from the .NET framework `bool <numeric type>.TryParse(string s, out <numeric type> result)` in that, instead of `result` being an `out` parameter, it is a `ref` parameter. We would then perhaps wrap it as:

```c#
/// <summary>
/// Attempts to parse a text to a <see cref="Complex"/> number. 
/// </summary>
/// <remarks>
/// <para>
/// The provided <see cref="Complex.TryParse(string, ref Complex)"/> method requires the result
/// to have been created which differs from the norm.
/// </para>
/// </remarks>
/// <param name="s">The text to parse into complex.</param>
/// <param name="result">The parsed valued if the parsing was successful.</param>
/// <returns><c>True</c> if the parsing was successful.</returns>
internal static bool TryParseComplex(string s, out Complex result)
{
    result = new Complex();
    return Complex.TryParse(s, ref result);
}
```

Although I don't want to make a case for what is "obvious" code, I would also encourage not to add comments explaining syntax or language features no matter how obscure or complicated these are. For instance:

```c++
/* "identifier" is a constant pointer (cannot point to a different location) 
 * to a constant int (its value cannot be modified).
 */
int const * const identifier = ...;
```

Perhaps, not commenting something like this will encourage both the author and the maintainer to agilize their minds–through repetition–such that even more complicated syntax would come as naturally as `int identifier = ...`.

