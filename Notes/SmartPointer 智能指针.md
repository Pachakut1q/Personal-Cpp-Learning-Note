### 智能指针(SmartPointer)
C++使用内存的时候很容易出现野指针、悬空指针、内存泄露的问题。所以C++11引入了智能指针来管理内存。  
1.unique_ptr  
当超出作用域时自动被销毁并调用delete；  
不能复制一个unique_ptr，因为复制过后两者指向的是同一个内存，当其中一个指针被销毁时，所指向的内存空间也被释放了，会出现所谓“悬空指针”的未定义行为;  
最简单的智能指针，几乎没有开销，只是一个栈分配对象。  
```
std::unique_ptr<Entity> entity = std::make_unique<Entity>();
std::unique_ptr<Entity> entity(new Entity()); //valid
```
2.shared_ptr  
通过引用计数，跟踪指针有多少个引用，当计数为0时，被销毁;  
shared_ptr需要分配另一块内存，叫做控制块，用来存储引用计数；  
```
std::shared_ptr<Entity> sharedEntity = std::make_shared<Entity>();
std::shared_ptr<Entity> sharedEntity(new Entity());//valid but not good
//先创建一个Entity将其传递给shared_ptr构造函数，需要一次内存分配，然后shared_ptr的控制内存块也要分配。使用make_shared可以将其组合起来更有效率。
```
3.weak_ptr  
用于解决shared_ptr的循环引用问题，即当两个或多个对象通过shared_ptr互相引用时，它们的引用计数永远不会归零，导致内存泄漏；  
weak_ptr不会增加引用计数，因此不会阻止对象的销毁；  
```
std::weak_ptr<Entity> weakEntity = sharedEntity;
```
