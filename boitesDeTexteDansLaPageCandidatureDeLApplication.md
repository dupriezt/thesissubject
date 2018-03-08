BOITES DE TEXTES DANS LA PAGE CANDIDATURE DE L'APPLICATION (utilisées pour la feuille de résumé du sujet de thèse)
# Résumé du sujet de thèse

Large and complex industrial applications have a lifetime of 15 to 25 years. Bugs arrive daily in any application that is large enough and needs to evolve to adapt to new requirements. Identifying bugs is a really time consuming task. In this PhD we will (1) explore the idea of back-in-time debuggers, able to step executions backward, (2) explore new ways to debug applications by comparing program executions and (3) design a domain specific language to help developer automatise debugging sessions.

# Contexte sociétal, économique et/ou industriel

According to a study conducted by the Judge Business School at Cambridge University and in collaboration with Cambridge-based Undo Software and Rogue Wave Software companies, the global cost of debugging software has risen to $312 billion annually. The study found that, on average, software developers spend 50% of their programming time finding and fixing bugs. When projecting this figure onto the total cost of employing software developers, this inefficiency is estimated to cost the global economy $312 billion per year.
B. Hailpern and P. Santhanam mention that testing and debugging are often more than 50% of project total cost.
I. Sommerville and A. Zeller also underline that identifying and fixing bugs is a time-consuming activity.

What this all amounts to is that debugging is a considerably time-consuming and expensive activity in the software industry, meaning that supporting developers with better debugging tools is a research area of interest for the software development sector and has a high potential for practical application.

# Contexte Scientifique

Mainstream debuggers allow developers to place breakpoints in their code. When an execution reaches a breakpoint, the debuggers stops it and shows the developer the stack trace: the list of in-progress method calls ("stack frame") starting with the "main" method and ending with the method containing the breakpoint. In addition, debuggers allow to step the execution forward and inspect stack frames (to see the values of the variables defined in them for example).

Several works have been proposed to help developers with the task of debugging.
Some approaches propose execution dice-based fault localization. The basic idea is to compare execution paths.
Automatic validation of conditions and watchpoints help developers to spot divergences from the expected program execution.
Back-in-time debuggers offer the possibility to navigate the program execution history with several promising research results.
More recently, object-centric debuggers presented advanced stepping mechanisms targeting individual objects.
Moldable debuggers offer a different perspective to this problem: allowing programmers to adapt a debugger to a given domain or task. 

As for my personal experience, I did an M2 internship and am currently doing a research year on the subject of debugging. During these, I published a position paper about new debugger features and prototypes at the IWST workshop of ESUG 2017. I prototyped a tool to instrument methods so that the values of their expressions are recorded and can be browsed later by the developer. I prototyped another tool allowing developers, with some limitations, to define an invariant on their program, run it, and have a debugger open on the instruction where the invariant stops being true. I developed an IDE plugin for the Pharo language (http://www.pharo.org) listing all breakpoints of the system, allowing to toggle them on/off with a click via either automatic code rewriting or bytecode manipulation. I collaborated with Marcus Denker (CR1) to improve the conditional breakpoints of Pharo to have their conditions be executed "as if" they were in the context the breakpoints were placed in, which involved context forwarding and AST manipulation techniques. I implemented a pharo AST interpreter to control the execution and develop prototype of debugging tools using this. Finally, I am currently collaborating on a debugger project for big data systems, and a formal semantics of a debugger for concurrent programs.

# Démarche

The goal of this thesis is to research new debugging techniques to aid software developers detecting and correcting defects.
We plain to approach this research by exploring three different axis: 1) back-in-time debugging, 2) execution comparison and 3) debugging specific programming languages.

Each of these axis represents a promising, but challenging to precisely define and implement, debugging feature. However, the objective is not to develop new debugging features in a vacuum, but rather to build them in real development scenarios. For this reason, we intend to organize our work in agile cycles of ~6 months each. Each cycle will comprise the following steps:
1) Review of the existing literature on a debugging feature
2) Prototyping the feature
3) Validation of the prototype with real industrial developers
4) Adjustments based on the feedback
5) Publication

Back in time debuggers.
A back in time debugger is a debugger that can go backward in an execution. This is especially useful to answer questions like "where does this value come from?" or to find the cause of a bug when it is no longer on the execution stack. The main challenge of designing a back in time debugger is to find the right trade-off between storing the execution in memory (leading to important memory usage and overhead) and re-executing it when needed (leading to latency when using the debugger and tricky cases when dealing with network requests, OS calls...).

Execution comparison.
An important category of bugs are regressions: a program that used to pass a given test is modified and no longer passes it. In a slightly different scenario, a program could fail on a particular input, while working on another input. To assist developers in these debugging scenarios, the execution comparison feature would allow them to debug both executions (the one that works and the one that does not) concurrently, with adapted debugging operations like Step to the next difference, to get a better understanding of what is different between them: what makes the second execution fail?
As a starting point, we would look into the question of how to compare two living execution stacks, and extend existing tools to visualise executions side-by-side.
The main challenges for this feature are:
1) what is a definition of "difference" between two executions that would be useful for debugging?
2) How to recognise matching objects between the two executions (by their state? by how they have been used in the executions?)?

Debugging specific language.
Mainstream debuggers offer basic step commands like "step over" or "step into" as buttons. The idea behind this feature is to give the developer the ability to control the debugger via a Domain Specific Language. For example, this will allow the developer to craft his own step commands like "step into until reaching an object of class C" or "step over until variable V has value W", to adapt to the particular application that is debugged. A console would be integrated into the user interface of the debugger to give the developer instant access to this potential. Additionally, the debugger could record the step operations performed by the developer so that they can be shared with others to reach a particular point in an execution. The challenges for this feature are: how to design a language that is convenient to use for developers and make their lives easier, what are the basic stepping operations needed so that this DSL can get re-used for other debuggers, how to integrate it with the other two axis of this thesis to allow to script the step back in time and the debugging of two similar execution
As a starting point, we would prototype the scripting language with notably 1) access to the basic step operations of debuggers 2) inclusion of the power of general programming languages (loops, if-then-else constructs...) 3) inclusion of a mean to easily define patterns on the execution stack or the states of objects, to be used as stopping conditions, or patterns to step over for example.  

Mainstream debuggers offer basic step commands like "step over" or "step into" as buttons.
We propose the development of a debugging specific language (DbSL) to give the developer the ability to programmatically control the debugger.
For example, this will allow the developer to craft his own step commands like "step into until reaching an object of class C" or "step over until variable V has value W", to adapt to the particular application that is debugged.
Additionally, the debugger could record the step operations performed by the developer so that they can be reused as debugging macros and shared with others to reach a particular point in an execution. 
As a starting point, we would prototype the scripting language with notably 1) access to the basic step operations of debuggers 2) inclusion of the power of general programming languages (loops, if-then-else constructs...) and 3) the ability to easily define patterns on the execution stack or the states of objects, to be stepped over or used as stopping conditions.

The main challenges for this feature are:
1) How to design a language that is convenient to use for developers and make their lives easier?
2) What are the basic stepping operations the underlying debugger needs to provide to the DbSL? Can we re-use this DbSL with different existing debuggers?
3) How to integrate it with the other two axis of this thesis to allow developers to script the stepping back in time and the debugging of two similar executions?


# Actions prévues pour la première année

Work on the execution comparison and debugging specific languages axis (see Démarche section for more information).

# Actions prévues pour la deuxième année

Work on the back in time debuggers axis (see Démarche section for more information).