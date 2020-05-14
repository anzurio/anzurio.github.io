---
layout: post
title: Get to Know Your Compiler
---

[^1]: Originally written for Propelics and currently [published](https://www.anexinet.com/blog/talking-code-get-to-know-your-compiler/) at Anexinet's Blog.

[^1] Given a non-trivial task with many solution paths, a sensible Computer Scientist, would accomplish it through the path which offers the best time and space complexity balance. A seasoned Software Engineer would also understand that, getting the task done, is but half of the job; the resulting code must also be maintainable. One way to accomplish this is by making the source readable by others and it is thanks to the work of the former that the latter can spend most of its time designing a readable framework to perform a task without having to worry—at least too much—about macro-optimizing their programs.

I am talking about how the compiler provides a full range of optimization that most of us are not even aware of. Just like the introduction of context-free  language to machine code compilers made early computer programming more human-understandable, so do modern compilers today by optimizing the generated machine code to be more efficient without needing the programmer to device obfuscated code to improve performance. 

For instance, take a task to be accomplished programmatically where the size of the output can be disregarded; the major concern is its performance to the tick of the processor.  One may very well think that, in order to save ticks on stack operations, achieve the task within a very long processing unit (i.e., a function). This would go against the programming adage of making a function do one thing and one thing only; modulating code into functions makes it more maintainable even if those functions are called just once. If we were to do this task on C++ for instance, we could take advantage of GNU C++ Compiler’s optimizing options for heuristically inlining functions: `-finline-functions`, `-finline-small-function`, and `-finline-functions-called-once` depending on the specifics of the task at hand.

Another example of when it is wise to mind the compiler comes as to the debate of whether to pre-fetch the size of a collection when looping through it. Compare the following snippets of code:

<table>
<tr><td>

```csharp
int len = args.Length;                    
for (int i = 0; i < len; i++)
{
    Console.WriteLine(args[i]);
}
```

</td>
<td>

```csharp
for (int i = 0; i < args.Length; i++)
{
    Console.WriteLine(args[i]);
}
```

</td>
</tr>
</table>

Without knowing too much about neither the language nor the compiler, one would assume that, the one on the left might generate more efficient code. After all, it seems that the other snippet will evaluate args.Length every iteration. In C#, it is not so; take a look at the optimized code emitted after the Just In Time Compiler has had it pass at it (I have omitted interrupt instructions which allowed me to see the code after JIT):

<table>
<tr><td>

```assembly
;int len = args.Length;
    push        ebp  
    mov         ebp,esp  
    push        edi  
    push        esi  
    push        ebx  
    mov         edi,ecx    
    pop         edi  
    add         al,33h  
;for (int i = 0; 
    test        byte ptr [ebp-74F18125h],4Ch  
;Console.WriteLine(args[i]);
    003D04F9:
    mov         bh,8  
    call        722F0ADC  
;i++)
    inc         esi  
;i < len; 
    cmp         esi,ebx  
    jl          003D04F9
```

</td>
<td>

```assembly
;for (int i = 0; 
    push        ebp  
    mov         ebp,esp  
    push        edi  
    push        esi  
    push        ebx  
    mov         edi,ecx  
;i < args.Length; 
    mov         ebx,dword ptr [edi+4]  
    test        ebx,ebx  
    jle         001B0507  
;Console.WriteLine(args[i]);
    001B04F9:
    mov         ecx,dword ptr [edi+esi*4+8]  
    call        722F0ADC  
;i++)
    inc         esi  
;i < args.Length; 
    cmp         ebx,esi  
    jg          001B04F9
    001B0507:
```

</td>
</tr>
</table>

Even with no experience in Assembly, one can notice that the code generated is similar in length and form and, most importantly, the portion that gets looped over is too. One might wonder why the mov instructions on line 14 differ greatly on their operands and that not every CISC instruction executes at a constant rate but, suffice to say, this does not impact the speed of execution in this example’s end product; the way assemblers generate machine code is outside of this post’s scope.

At a glance, these examples, may seem trivial but do help make the point of encouraging the reader to take a closer look at what their compiler of choice does behind the scenes thus, allowing the engineer to focus most of their effort on making their code more readable.

