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
### 多维数组
```
int main()
{
    // 二维数组
	int** a2d = new int* [5];
	for (int i = 0; i < 5; i++)
	{
		a2d[i] = new int[5];
	}

    // 三维数组
	int*** a3d = new int** [5];
	for (int i = 0; i < 5; i++)
	{
		a3d[i] = new int*[5];
		for (int j = 0; j < 5; j++)
		{
			a3d[i][j] = new int[5];
			//相当于
			//int** ptr = a3d[i];
			//ptr[j] = new int[5];
		}
	}

    //释放二维数组堆内存
	for (int i = 0; i < 5; i++)
	{
		delete[] a2d[i];
	}
	delete[] a2d;

    //释放三维数组堆内存
	for (int i = 0; i < 5; i++)
	{
		for (int j = 0; j < 5; j++)
		{
			delete[] a3d[i][j];
		}
		delete[] a3d[i];
	}
	delete[] a3d;
	std::cin.get();
	return 0;
}
```
所以其实C++中的多维数组创建是较为麻烦的。上述代码中创建了一个5*5的二维数组，实际上是创建了5个单独的缓存块，每块5个int，并不是连续分配的内存。当读写数据时可能会导致cache miss，访问速度也会变慢。  
可以用一维数组来表示多维数组，以二维数组为例
```
int* array = new int[5 * 5];
for (int x = 0; x < 5; x++)
{
	for (int y = 0; y < 5; y++)
	{
		array[x * 5 + y] = 1;
        // 每5个一组
	}
}
```
