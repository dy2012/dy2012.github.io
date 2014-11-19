---

layout: post  

title:  main thread pthread\_exit

tags: [linux]

---

当一个POSIX threads process的主线程调用pthread\_exit，而其它线程继续运行时，进程会继续停留，直到遇到下面三种情况才会终止：

* 所有其他的线程也调用pthread\_exit
* 它们中的一个调用\_exit或exit
* 进程异常终止

在这期间，如果进程正常运行，同时defunct进程不在进程列表中出现，而POSIX的任务调度控制在列表中，那将会是比较理想的情况。


    #include <stdlib.h>
    #include <stdio.h>
	#include <unistd.h>
	#include <pthread.h>
	
	#define NUM_THREADS 5
	
	void 
	*task(void *a)
	{
		sleep(10);
		pthread_exit(NULL);
	}
	
	int
	main(int argc, char *argv[])
	{
		pthread_t thr[NUM_THREADS];
		int i;
		
		for (i = 0; i < NUM_THREADS; i++) {
			if (pthread_create(&thr[i], NULL, task, 0) != 0) {
				fprintf(stderr, "pthread_create failed\n");
				return EXIT_FAILURE;
			}
	  }
	
		pthread_exit(NULL);     //main pthread 立即结束
	}


然后查看是否有defunct的进程，
    

	$ps -ef | grep a.out

	dy        3566  2558  0 09:00 pts/1    00:00:00 [a.out] <defunct>
	dy        3573  3229  0 09:00 pts/0    00:00:00 grep funct

当主线程调用pthread\_exit时，进程并没有立即退出，尽管它还有正在运行的线程，这时进程的状态是defunct。当所有线程都调用pthread\_exit时，才会被销毁。

产生defunct原因是因为主线程会在内核中从头至尾调用do_exit子程序，并使最后的调度调用变成僵尸进程。