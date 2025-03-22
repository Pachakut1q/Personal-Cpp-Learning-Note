### 引用 
引用是指针的“伪装”，是在指针上的语法糖。  
必须引用已存在的变量，引用本身不是新的变量，没有真正的存储空间。  
一旦被创建就无法改变引用的是哪个变量。  
```
int a = 5;
int& ref = a;
ref++;
//Now a=ref=6
```
```
void increment(int& a)
{
  a++;
}
int main()
{
  int a = 5;
  increment(a);
  std::cout << a << std::endl;
}//Print 6
```

