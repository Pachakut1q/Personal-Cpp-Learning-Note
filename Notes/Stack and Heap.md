### Stack and Heap
1.内存管理  
stack自动分配和释放，由编译器自动管理。当函数被调用时，局部变量在栈上分配；函数返回时，内存自动释放。  
heap手动分配和释放。需要通过new/malloc显式申请内存，通过delete/free显式释放内存。  
2.分配速度  
stack仅需移动栈指针即可完成内存分配。严格按照顺序分配和释放，不会产生内存碎片。  
heap需要寻找合适的内存块，可能触发系统调用。频繁的new/delete会导致内存碎片，降低分配效率。  
3.内存容量  
stack固定大小，通常较小。有溢出风险，过度分配会导致栈溢出。  
heap动态扩展，可用内存取决于系统资源。适合大对象，可分配大型数据结构。  
4.访问方式  
stack通过变量名直接操作，heap必须通过指针。  
5.异常安全性  
stack自动清理，函数抛出异常时，栈上的对象会通过栈展开自动调用析构函数。  
heap若在 new 和 delete 之间发生异常，可能导致内存泄漏（需用智能指针如 std::unique_ptr 规避）。
6.多线程环境  
每个线程有独立的栈，无需同步。  
所有线程共享堆内存，需通过锁或原子操作保证线程安全。  
  
### 内存碎片
内部碎片(Internal Fragmentation)：已分配给程序的内存块中，未被实际使用的部分。内存分配器按固定大小（如页、块）分配内存，若程序申请的内存小于分配单元，剩余空间会被浪费。比如固定大小的内存池分配。  
外部碎片(External Fragmentation)：内存中存在大量分散的小块空闲区域，无法合并成连续的大块内存以满足程序需求。频繁的动态内存分配和释放（如 new/delete 或 malloc/free）导致空闲内存被切割为不连续的小块。比如堆内存、长期运行的程序频繁地分配和释放不同大小的内存。