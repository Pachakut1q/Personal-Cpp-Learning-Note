### 创建对象
两种方式  
```
//堆对象（需手动释放）
Entity* e = new Entity();
e->GetName();  //通过指针访问
delete e;      //必须手动释放否则发生内存泄漏
/*
Entity* e2 = e;
delete e2;	   //e和e2指向的是同一处堆内存空间，只需要delete其中一个即可
*/
//栈对象（自动释放）
Entity e1 = Entity();//just "Entity e1" in C++17
e1.GetName();  //直接访问
// e1 在离开作用域时自动调用析构函数
```
如何选择？对象太大或显式控制对象的生存期就在heap上创建，否则创建在stack
