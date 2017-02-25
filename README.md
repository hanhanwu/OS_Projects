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
* The author's presentation (it's good but does not include all main points in the paper, but my presentation needs to include them all....): https://www.youtube.com/watch?v=mqTgGUtwHLU
* More detailed explaination: https://people.cs.umass.edu/~emery/pubs/Novark-PhD-thesis.pdf
* Find details of different computer virus: http://virus.wikidot.com/ramen
* PPT from the paper authors: http://slideplayer.com/slide/8844764/
* PPT from Archipelago paper: http://slideshowes.com/doc/360854/archipelago--trading-address-space-for-reliability-and
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
   
   
 * Heap Spraying Attacks - make exploitation of other volunerabilities easier
   1. <b>ASLR</b> - Address space layout randomization (ASLR) is a memory-protection process for operating systems (OSes) that guards against buffer-overflow attacks by randomizing the location where system executables are loaded into memory. It makes guessing the location of heap-allocated shellcode or the address of a specific function for a return-to-libc attack more difficult.
   
   2. A <b>“return-to-libc”</b> attack is a computer security attack usually starting with a buffer overflow in which a subroutine return address on a call stack is replaced by an address of a subroutine that is already present in the process’ executable memory, bypassing the NX bit feature (if present) and ridding the attacker of the need to inject their own code.
   
   3. [Heap spraying][10], [Heap Spray in history][13], [Heap Spray details and tutorial...][14], [Arbitary Code Execution][11], [Arbitary code Execution results][12], [Shellcode][9]
   
   4. Heap Spraying Attack Model - no knowledge/know valid heap object address. [Archipelago Allocator][15]
   
   5. [!!! Heap Spray and Heap Feng Shui PPT][16]
   
 * Dangling Pointer Attacks
   1. [Dangling Pointer and the troubles it can bring][21]
   
   2. [Heap Defragmentation Explaination][22], [conservative garbage collection][23], [GUN][24], [Pine Mail Reader][25], [squid web proxy][26]
   
   3. bftpd: The Bftpd program is a small, flexible FTP server which is designed to work out of the box with little or no configuration required. Most users in home and small office environments can simply install Bftpd without any manual configuration, Bftpd will automatically attempt to work as smoothly and securely as possible.
   
   4. thttpd: (tiny/turbo/throttling HTTP server) is an open source software web server from ACME Laboratories, designed for simplicity, a small execution footprint and speed.
   
   5. OpenSSH: (also known as OpenBSD Secure Shell [a]) is a suite of security-related network-level utilities based on the Secure Shell (SSH) protocol, which help to secure network communications via the encryption of network traffic over multiple authentication methods and by providing secure tunneling capabilities.
 
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

* Demo for intra-procedural (not branch aware): https://github.com/nsumner/llvm-dataflow-analysis
* Intraprocedural Analysis - Individual functions are analyzed in isolation
* Interprocedural Analysis - By considering interactions between calling and called procedures, analyze the whole program
* Data-flow analysis is a technique for gathering information about the possible set of values calculated at various points in a computer program. A program's control flow graph (CFG) is used to determine those parts of a program to which a particular value assigned to a variable might propagate. The information gathered is often used by compilers when optimizing a program. [Wiki defination][8]
* [Finite State Machine (FSM)][17], [Turing Machine][18], [Turing Complete][19]
* [Description of ESP][20]

[1]:http://stackoverflow.com/questions/667177/heap-overflow-attacks
[2]:http://www.cse.scu.edu/~tschwarz/coen152_05/Lectures/BufferOverflow.html
[3]:http://cis1.towson.edu/~cssecinj/links-resources/real-life-examples/#BO
[4]:http://stackoverflow.com/questions/1120575/what-is-the-difference-between-a-stack-overflow-and-buffer-overflow
[5]:http://www.qnx.com/developers/docs/qnxcar2/index.jsp?topic=%2Fcom.qnx.doc.neutrino.prog%2Ftopic%2Fhat_OverrunErrors.html
[6]:https://en.wikipedia.org/wiki/Buffer_overflow_protection#Canaries
[7]:https://en.wikipedia.org/wiki/Address_space_layout_randomization#OpenBSD
[8]:https://en.wikipedia.org/wiki/Data-flow_analysis
[9]:https://en.wikipedia.org/wiki/Shellcode
[10]:https://en.wikipedia.org/wiki/Heap_spraying
[11]:https://en.wikipedia.org/wiki/Arbitrary_code_execution
[12]:http://www.pctools.com/security-news/arbitrary-code-execution/
[13]:http://ecee.colorado.edu/~ekeller/classes/fall2014_advsec/papers/heap-sprays-to-sandbox-escapes_issa0113.pdf
[14]:https://www.corelan.be/index.php/2011/12/31/exploit-writing-tutorial-part-11-heap-spraying-demystified/
[15]:https://people.cs.umass.edu/~emery/pubs/archipelago.pdf
[16]:http://www.blackhat.com/presentations/bh-europe-07/Sotirov/Presentation/bh-eu-07-sotirov-apr19.pdf
[17]:https://en.wikipedia.org/wiki/Finite-state_machine
[18]:https://en.wikipedia.org/wiki/Turing_machine
[19]:https://en.wikipedia.org/wiki/Turing_completeness
[20]:http://www.cs.cornell.edu/courses/cs711/2005fa/slides/sep27.pdf
[21]:https://en.wikipedia.org/wiki/Dangling_pointer
[22]:http://openscholarship.wustl.edu/cgi/viewcontent.cgi?article=2031&context=cse_research
[23]:http://stackoverflow.com/questions/7629446/conservative-garbage-collector
[24]:https://en.wikipedia.org/wiki/GNU
[25]:https://en.wikipedia.org/wiki/Pine_(email_client)
[26]:https://en.wikipedia.org/wiki/Squid_(software)


******************************************************

Critique 2

* https://github.com/hanhanwu/OS_Projects/blob/master/etst_case_for_specific_mining.pdf
* https://github.com/hanhanwu/OS_Projects/blob/master/invariants-tse2001.pdf


******************************************************

Final Project

Data Science Methods
* Machine Learning Applications: https://www.swe.informatik.uni-goettingen.de/research/machine-learning-applications-software-engineering
* Detection of feature freezes using clustering algorithms: https://pdfs.semanticscholar.org/a128/5d1471d58f61c156f09fc8596e36cd5c4802.pdf
* Python Predictive Analysis for bug detection: http://researcher.watson.ibm.com/researcher/files/us-liup/Python%20Predictive%20Analysis%20for%20Bug%20Detection.pdf
* Machine Learning for Programming
 * All papers/talks: http://www.srl.inf.ethz.ch/spas
 * dataset: http://www.srl.inf.ethz.ch/py150
 * Probabilistic Model for Code with Decision Trees: http://www.srl.inf.ethz.ch/papers/oopsla16-dt.pdf
* BigDubug
 * Debug Spark paper: http://web.cs.ucla.edu/~miryung/Publications/icse2016-gulzar-bigdebug.pdf
 * Their API (currently only support RDD, and looks like scala only): https://sites.google.com/site/sparkbigdebug/api

Machine Learning & Cyber Security 
* Good papers: http://www.kdnuggets.com/2017/01/machine-learning-cyber-security.html
* NN crack: https://www.usenix.org/system/files/conference/usenixsecurity16/sec16_paper_melicher.pdf
* Anomalous Payload-based Network Intrusion Detection: http://www.covert.io/research-papers/security/PAYL%20-%20Anomalous%20Payload-based%20Network%20Intrusion%20Detection.pdf
* Exploiting machine learning to subvert your spam filter: https://people.eecs.berkeley.edu/~tygar/papers/SML/Spam_filter.pdf
* SpamBayes: http://spambayes.sourceforge.net/
* Network intrusion detection guidelines, challenges of machine learning in this area: https://www.utdallas.edu/~muratk/courses/dmsec_files/oakland10-ml.pdf


Auto Source Code Analysis Tools:
* PyChecker (debug): http://legacy.python.org/workshops/2002-02/papers/02/
* List of python code metrics tools (code metrics, bug report): https://www.fullstackpython.com/code-metrics.html
* PyMetrics (code metrics): https://sourceforge.net/projects/pymetrics/
* Python randon (code metrics): https://pypi.python.org/pypi/radon
* code Climate Engine (code metrics for python, JavaScript, ruby and php): https://docs.codeclimate.com/docs/switching-to-code-climate-platform#python-analysis


StackOverflow Related Program Analysis
* Make a good code example: https://www.semanticscholar.org/paper/What-makes-a-good-code-example-A-study-of-Nasehi-Sillito/b8f9539d145638ac93957da4f653e238a4e9d413
* Building reputation in StackOverflow: an empirical investigation: https://www.semanticscholar.org/paper/Building-reputation-in-StackOverflow-an-empirical-Bosu-Corley/343edae0cab9a649ad61d1c5ce36b20b52ae66df
* Tag Recommendations in StackOverflow: https://www.semanticscholar.org/paper/Tag-Recommendations-in-StackOverflow-Short-Wong/025734094e6f1a166ba29c0b50f06d0e50fe116b
* Selection and presentation practices for code example summarization: https://www.semanticscholar.org/paper/Selection-and-presentation-practices-for-code-Ying-Robillard/84083ccc9e2a8f6f7341c9166f80c8e1b3e25c74
* Subjective Evaluation of Software Quality Using Crowdsource Knowledge: An Exploratory Study: https://www.semanticscholar.org/paper/Subjective-Evaluation-of-Software-Quality-Using-Rahman-Roy/d21302a9e6e85409d490781f8e378ecb390b0170


Stackoverflow API
* https://api.stackexchange.com/docs
