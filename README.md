# OS_Projects
god bless me, finger cross


Small Project 1

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

