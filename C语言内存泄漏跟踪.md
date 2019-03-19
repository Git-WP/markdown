### C语言内存泄漏跟踪

#### mtrace

GNU C提供了跟踪动态内存泄漏的接口，定义在`mcheck.h`头文件中，函数原型如下所示：

```c
#include <mcheck.h>
void mtrace(void);
void muntrace(void);
```



在Linux Programmer's Manual中对`mtrace`的描述如下：

> The mtrace() function installs hook functions for the memory-allocaion functions(malloc, realloc, free). These hook functions record tracing information about memory allocation and deallocation. The tracing information can be used to discover memory leaks nad attempts to free nonallocated memory in a program.



使用`mtrace`前需要设置环境变量`MALLOC_TRACE`：

```c
MALLOC_TRACE=/your/path/to/file.txt
export MALLOC_TRACE
```



在你的`program`需要进行跟踪的地方调用`mtrace`,通常不需要调用`muntrace`.  `mtarce`的输出需要使用GNU C库提供的一个Perl脚本`mtrace`进行转换，变成可读的形式。

```c
mtrace program file.txt
```



`mtrace`可以跨模块工作，且是线程安全的。