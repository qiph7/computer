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
