# OS_Projects
god bless me, finger cross


Small Project 1

* Demo: https://github.com/nsumner/llvm-demo
* Assignment: https://github.com/nsumner/callgraph-profiler-template

* CMake: CMake is an extensible, open-source system that manages the build process in an operating system and in a compiler-independent manner. Unlike many cross-platform systems, CMake is designed to be used in conjunction with the native build environment.
* Install cmake on Mac: http://tudat.tudelft.nl/projects/tudat/wiki/Install_on_Mac_OS_X
* LLVM: The LLVM compiler infrastructure project (formerly Low Level Virtual Machine) is a "collection of modular and reusable compiler and toolchain technologies" used to develop compiler front ends and back ends.
* LLVM Programmer Manual: http://llvm.org/docs/ProgrammersManual.html
* LLVM Language Reference Manual: http://llvm.org/docs/LangRef.html
* Bitcode is an intermediate representation of a compiled program.
* IR - Intermediate Representation code, the heart of LLVM, https://idea.popcount.org/2013-07-24-ir-is-better-than-assembly/
* SSA -  static single assignment form is a property of an intermediate representation (IR), which requires that each variable is assigned exactly once, and every variable is defined before it is used.
* LLVM has phi instruction with quite weird explanation: The 'phi' instruction is used to implement the φ node in the SSA graph representing the function. Typically it is used to implement branching.
* Building LLVM with CMake: http://llvm.org/docs/CMake.html
* About "Instruction": http://www.cplusplus.com/doc/tutorial/introduction/
* LLVM Pass: The LLVM Pass Framework is an important part of the LLVM system, because LLVM passes are where most of the interesting parts of the compiler exist. Passes perform the transformations and optimizations that make up the compiler, they build the analysis results that are used by these transformations, and they are, above all, a structuring technique for compiler code. http://llvm.org/docs/WritingAnLLVMPass.html
* LLVM Module: The Module class represents the top level structure present in LLVM programs. An LLVM module is effectively either a translation unit of the original program or a combination of several translation units merged by the linker. The Module class keeps track of a list of Functions, a list of GlobalVariables, and a SymbolTable. Additionally, it contains a few helpful member functions that try to make common operations easy. http://llvm.org/docs/ProgrammersManual.html#the-globalvariable-class
* GlobalVariable(const Type *Ty, bool isConstant, LinkageTypes &Linkage, Constant *Initializer = 0, const std::string &Name = "", Module* Parent = 0)
 * Create a new global variable of the specified type. If isConstant is true then the global variable will be marked as unchanging for the program. The Linkage parameter specifies the type of linkage (internal, external, weak, linkonce, appending) for the variable. If the linkage is InternalLinkage, WeakAnyLinkage, WeakODRLinkage, LinkOnceAnyLinkage or LinkOnceODRLinkage, then the resultant global variable will have internal linkage. AppendingLinkage concatenates together all instances (in different translation units) of the variable into a single variable but is only applicable to arrays. See the LLVM Language Reference for further details on linkage types. Optionally an initializer, a name, and the module to put the variable into may be specified for the global variable as well.
* BasicBlock(const std::string &Name = "", Function *Parent = 0)
 * The BasicBlock constructor is used to create new basic blocks for insertion into a function. The constructor optionally takes a name for the new block, and a Function to insert it into. If the Parent parameter is specified, the new BasicBlock is automatically inserted at the end of the specified Function, if not specified, the BasicBlock must be manually inserted into the Function.
* LLVM CallSite functions: http://llvm.org/docs/doxygen/html/CallSite_8h_source.html

* This project cost me whole week and forced me to work in the lab almost all the time till 11 pm each day.... What the hell, there are 2 more "small projects".... I don't want to touch anything related to OS or C or C++ in the rest of my life (after school graduation) any more!
* But, still have to work very hard, I chose it because I want to learn more about cyber security, all for my career future. At least go though C++ tutorials first: https://www.tutorialspoint.com/cplusplus/


******************************************************

Presentation 1 - Die Harder: Securing The Heap

* The paper: https://people.cs.umass.edu/~emery/pubs/ccs03-novark.pdf
* According to the authors, Die Harder provides the highest level of security from heap-based memory attacks
* Memory Allocators (find images/short videos which could describe how do they work quickly)
 * Freelist-based Allocators
 * BiBOP-style Allocators
* Threat Model
 * Draw an image of the worst case for prime attack targets
 * Find an easy-to-understand emaple in the real world if there was any
* Attacks (find image/video/real world examples of the attacks, how do they work)
 * Background Knowledge
   1. Typical modern software systems allocate memory dynamically from structures known as <b>heaps</b>. Calls are made to heap-management routines to allocate and free memory. Heap management involves some computation time and can be a performance issue. <b>Chunking</b> refers to strategies for improving performance by using special knowledge of a situation to aggregate related memory-allocation requests.
 * Heap Overflow Attacks
   1. A <b>heap overflow</b> is a type of buffer overflow that occurs in the heap data area. <b>Exploitation</b> is performed by corrupting this data in specific ways to cause the application to overwrite internal structures such as linked list pointers. [How does it work when an attacker replaces the function return address with his address][1]. 
   
   2. Early Attacks: attack targeted application. The attack forces the allocator to allocate the source chunk and victim chunk contiguously. Then overflows the buffer, overwritting the function pointer with an attacker-controlled address. [Heap Overflow, Stack Overflow and Buffer Overflow][2], [Differences between the 3 attacks][4], [Real life buffer overflow example][3]
   
   3. Freelist metadata attacks: The attack applies to any allocation that embeds freelist pointers directly in the freed chunks.Once a free chunk is corrupted, the attacker can simply force allocation until the chunk is reused.
   
   4. Other metadata attacks: attack the metadata resides at the beginning of some pages, attackers do not directly control target chunks but the target chunk contains these pages info structure.
   
   5. Allocator features that make them vulnerable to the overflow attack: Inline metadata, Page-resident metadata, Guard pages ([underrun and overrun][5]), Canaries ([Canaries wiki defination][6]), Randomized placement ([Randomized placement wiki defination][7])
   
 * Heap Spraying Attacks
 * Dangling Pointer Attacks
* Countermeasures used to address the volerabilities above (find a real world example)
* Die Harder Design (find image/video that contains the following components)
 * Sparse Page Layout
 * Address Space Sizing
 * Destroy-on-free
* Die Harder Analysis (find an easy way to show)
 * overflows
 * heap sprays
* Die Harder Evaluation (maybe draw a table)
 * If necessary, talk about whether the evaluation is reasonable, after checking enough evidence
* Summarize Die Harder Strength, Weakness
 * Strength
 * Weakness and Related Work
 
 
******************************************************

Project 2 - Inter-procedure Dataflow Analysis

Today is Chinese New Year, I am struggling with understanding OS assignment...... (2017/1/27)

* Template: https://github.com/nsumner/llvm-dataflow-analysis
 

[1]:http://stackoverflow.com/questions/667177/heap-overflow-attacks
[2]:http://www.cse.scu.edu/~tschwarz/coen152_05/Lectures/BufferOverflow.html
[3]:http://cis1.towson.edu/~cssecinj/links-resources/real-life-examples/#BO
[4]:http://stackoverflow.com/questions/1120575/what-is-the-difference-between-a-stack-overflow-and-buffer-overflow
[5]:http://www.qnx.com/developers/docs/qnxcar2/index.jsp?topic=%2Fcom.qnx.doc.neutrino.prog%2Ftopic%2Fhat_OverrunErrors.html
[6]:https://en.wikipedia.org/wiki/Buffer_overflow_protection#Canaries
[7]:https://en.wikipedia.org/wiki/Address_space_layout_randomization#OpenBSD
