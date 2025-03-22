### 数组(Array)
```
int example[5];//栈上申请

int* another = new int[5];
delete[] another;//堆上申请必须释放空间

const int exampleSize = 5;
int example[exampleSize];//数组大小必须是在编译阶段就能识别的常数

std::artay<int,5> another;
arraySize = another.size();//使用array容器，自带越界检查
```
