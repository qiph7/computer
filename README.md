# computer
notes for computer organization and design

## 5.7 Virtual memory

**two motivations for virtual memory:**  
	1.to allow efficient and safe sharing of memory among multiple programs  
	2.to remove the programming burdens of a small, limited amount of main memory  
	
In virtual memory, the address is broken into a virtual page number and a page offset. The physical page number constitutes the upper portion of the physical address, while the page off set, which is not changed, constitutes the lower portion.  

**with the enormous miss penalty, key decisions in designing virtual memory systems:**  
	1.pages should be large enough to try to amortize the high access time.  
	2.organizations that reduce the page fault rate are attractive.  
	3.page faults can be handle in software.  
	4.write-through will not work, use write-back.  

**hardware/software interface**  
  the process's address place, resides in memory, define by its page table.  
  the operating system simply loads the page table register to point to the page table of the process it wants to make active.  
  Each process has its own page table,since diff erent processes use the same virtual addresses.  
  Th e operating system is responsible for allocating the physical memory and updating the page tables.  
  
**page fault**  
  the operating system usually creates the space on fl ash memory or disk for all the pages of a process when it creates the process, called the swap space.  
  At that time, it also creates a data structure to record where each virtual page is stored on disk.   
  This data structure may be part of the page table or may be an auxiliary data structure indexed in the same way as the page table.  
  
**reducing the storage of page tables:**  
  1.keep a limit register  
  2.segments for stack and heap  
  3.hashing function  
  4.multiple levels of page tables  
  5.page tables to be paged  

**What about Writes?**  
  write-through is impratical, use write-back, replace the dirty page.  
  
**Making Address Translation Fast: the TLB**  
  translation-lookaside table (TLB): keeps track of recently used translations.  
  If a miss in the TLB occurs, we must determine whether it is a page fault or merely a TLB miss.  
  TLB misses can be handled either in hardware or in software.  
  Aft er a TLB miss occurs, we will need to select a TLB entry to replace, randomly choosing.  
  
**Integrating Virtual Memory, TLBs, and Caches**  
  a memory reference can encounter three different types of misses: a TLB miss, a page fault, and a cache miss.  
  virtually addressed cache: the processor can index the cache with an address that is completely or partially virtual.  
  
**Implementing Protection with Virtual Memory**  
three baisc capacities to enable the operating system to implement the virtual memory system:  
  1.Support at least two modes that indicate whether the running process is a user process or an operating system process.  
  2.Provide a portion of the processor state that a user process can read but not write.  
  3.Provide mechanisms whereby the processor can go from user mode to supervisor mode and vice versa.  
  
change from P1 to P2: 
  1.change the page table register to point to P2’s page table.  
  2.clear the TLB.  
  clearing the TLB is insufficient, the alternative is to extend the virtual address space by adding the process identifier.(8-bit address space ID)  

**Handling TLB Misses and Page Faults**  
a TLB miss can indicate one of two possibilities:
  1.The page is present in memory, and we need only create the missing TLB entry.  
  2.The page is not present in memory, and we need to transfer control to the operating system to deal with a page fault.  
Handling a TLB miss or a page fault requires using the exception mechanism.  

Once the operating system knows the virtual address that caused the page fault, it must complete three steps:  
  1.Look up the page table entry using the virtual address and fi nd the location of the referenced page on disk.  
  2.Choose a physical page to replace; if the chosen page is dirty, it must be written out to disk before we can bring a new virtual page into this physical page.  
  3.Start a read to bring the referenced page from disk into the chosen physical page.  
  
**understanding program performance**  
  1.a program would be continuously swapping pages between memory and disk, called thrashing.
  2.variable page sizes to lower the TLB miss.
  
