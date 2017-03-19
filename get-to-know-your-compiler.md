## Get to Know Your Compiler

Given a non-trivial task with many solution paths, a sensible Computer Scientist, would accomplish it through the path which offers the best time and space complexity balance. A seasoned Software Engineer would also understand that, getting the task done, is but half of the job; the resulting code must also be maintainable. One way to accomplish this is by making the source readable by others and it is thanks to the work of the former that the latter can spend most of its time designing a readable framework to perform a task without having to worry—at least too much—about macro-optimizing their programs.

I am talking about how the compiler provides a full range of optimization that most of us are not even aware of. Just like the introduction of context-free  language to machine code compilers made early computer programming more human-understandable, so do modern compilers today by optimizing the generated machine code to be more efficient without needing the programmer to device obfuscated code to improve performance. 

For instance, take a task to be accomplished programmatically where the size of the output can be disregarded; the major concern is its performance to the tick of the processor.  One may very well think that, in order to save ticks on stack operations, achieve the task within a very long processing unit (i.e., a function). This would go against the programming adage of making a function do one thing and one thing only; modulating code into functions makes it more maintainable even if those functions are called just once. If we were to do this task on C++ for instance, we could take advantage of GNU C++ Compiler’s optimizing options for heuristically inlining functions: `-finline-functions`, `-finline-small-function`, and `-finline-functions-called-once` depending on the specifics of the task at hand.

Another example of when it is wise to mind the compiler comes as to the debate of whether to pre-fetch the size of a collection when looping through it. Compare the following snippets of code:
<table>
<tr><td>
```
int len = args.Length;                    
for (int i = 0; i < len; i++)
{
    Console.WriteLine(args[i]);
}
```
</td>
<td>
</td>
</tr>
</table>