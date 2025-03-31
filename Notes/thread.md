### thread
```
static bool s_Finished = false;

void DoWork()
{
	std::cout << "thread id = " << std::this_thread::get_id() << std::endl;
	while (!s_Finished)
	{
		std::cout << "Working...\n";
		std::this_thread::sleep_for(std::chrono::seconds(1));
	}
}

int main()
{
	std::thread worker(DoWork);

	std::cin.get();
	s_Finished = true;

	worker.join();
	std::cout << "Finshed" << std::endl;
	std::cout << "thread id = " << std::this_thread::get_id() << std::endl;

	std::cin.get();
	return 0;
}
```
调用了join()线程对象，必须等待该线程的“任务完成”后，才能返回；worker线程在main函数这个线程中调用了join函数，就必须等待join函数返回后才能继续运行，也就是被阻塞了。  
这段程序即，创建了worker的线程执行DoWork函数一直打印“Working”，主线程等待worker.join()返回，被阻塞。当s_Finished变为true，DoWork函数跳出循环执行完毕，join返回，主线程解除阻塞，执行join之后的代码。