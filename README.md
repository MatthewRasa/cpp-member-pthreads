#C++ Member Function POSIX Threads
Provides functions for running POSIX pthreads on C++ member functions.

Usage:
```cpp
------------------------------------------------------------------------
SomeClass.h
------------------------------------------------------------------------
class SomeClass {
public:
	void do_work();
	void do_work(void *data);
}
```
```cpp
------------------------------------------------------------------------
ThreadInfo.h
------------------------------------------------------------------------
class ThreadInfo {
public:
	char *get_name();
	char *get_desc();
	int get_count();
private:
	char *mp_name, *mp_desc;
	int m_count;
}
```
```cpp
------------------------------------------------------------------------
Main.cpp
------------------------------------------------------------------------
#include "SomeClass.h"
#include "ThreadInfo.h"
#include "mthread.h"

int main() {
	pthread_t thread; // pthread
	pthread_attr_t attr; // pthread attributes
	SomeClass *p_ref = new SomeClass(); // Pointer reference to calling object
	ThreadInfo *p_info = new ThreadInfo(); // Pointer to pthread info
	
	// Run a pthread on p_ref->do_work(p_info)
	mthread_create(&thread, &attr, p_ref, SomeClass::do_work, (void *) p_info);
	
	/* OR */
	
	// Run a pthread on p_ref->do_work()
	mthread_create(&thread, &attr, p_ref, SomeClass::do_work);

	pthread_join(&thread, NULL);
	
	delete p_ref;
	delete p_info;	

	return 0;
}
```
