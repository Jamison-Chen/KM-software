Interpretation (轉譯) 與 Compilation (編譯) 並非互斥的概念，很多 Interpreter 做的事情與 Compiler 有某些部分是很像的。

簡言之，一旦 compiler 將 [[程式語言理論/零碎筆記#^2ea556|高階程式語言]] 翻譯成 machine code 後，只要 source code 的內容沒有被更動，往後每次執行程式時就可以直接運行 machine code，而不需要再次編譯。

在 Interpreted language 的世界裡則是每次執行到一個 statement 或 function 時都要做翻譯的工作，也就是說若某個 function 被呼叫了 n 次，同樣一段程式碼就會被轉譯 n 次，即使這 n 次呼叫 function 所填入的參數是相同的。

然而現在的 Interpreter 其實已經非常有效率了，轉譯的眾多環節中，有些會被分離出來，之所以這麼做的原因是因為那些環節可以只做一次*（比如 type analysis，此處暫不詳述）*。

## Development cycle

During the software development cycle, programmers make frequent changes to source code. When using a compiler, each time a change is made to the source code, they must wait for the compiler to translate the altered source files and link all of the binary code files together before the program can be executed. The larger the program, the longer the wait.

By contrast, a programmer using an interpreter does a lot less waiting, as the interpreter usually just needs to translate the code being worked on to an intermediate representation.

Compiled code is generally less readily debugged as editing, compiling, and linking are sequential processes that have to be conducted in the proper sequence with a proper set of commands. For this reason, many compilers also have an executive aid, known as a [Make](https://en.wikipedia.org/wiki/Make_(software)) file and program. The Make file lists compiler and linker command lines and program source code files, but might take a simple command line menu input (e.g. "Make 3") which selects the third group (set) of instructions then issues the commands to the compiler, and linker feeding the specified source code files.

## Distribution

A compiler converts source code into binary instruction for a specific processor's architecture, thus making it less portable. This conversion is made just once, on the developer's environment, and after that the same binary can be distributed to the user's machines where it can be executed without further translation. A [cross compiler](https://en.wikipedia.org/wiki/Cross_compiler) can generate binary code for the user machine even if it has a different processor than the machine where the code is compiled.

An interpreted program can be distributed as source code. It needs to be translated in each final machine, which makes the program distribution independent of the machine's architecture. However, the portability of interpreted source code is dependent on whether **the target machine having a suitable interpreter**. If the interpreter needs to be supplied along with the source, the overall installation process is more complex than delivery of a monolithic executable since the interpreter itself is part of what need be installed.

## Efficiency

The main disadvantage of interpreters is that an interpreted program typically runs slower than if it had been compiled. It generally takes longer to run a program under an interpreter than to run the compiled code but it can take less time to interpret it than the total time required to compile and run it.

Interpreting code is slower than running the compiled code because the interpreter must analyze each statement in the program each time it is executed and then perform the desired action, whereas the compiled code just performs the action within a fixed context determined by the compilation. This [runtime](https://en.wikipedia.org/wiki/Run_time_(program_lifecycle_phase)) analysis is known as "interpretive overhead". Access to variables is also slower in an interpreter because the mapping of identifiers to storage locations must be done repeatedly at run-time rather than at [compile time](https://en.wikipedia.org/wiki/Compile_time).

![[Screen Shot 2022-10-18 at 1.12.13 AM.png]]

![[Screen Shot 2022-10-18 at 1.12.44 AM.png]]
