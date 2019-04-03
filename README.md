willxin1024 批注：
1、代码中使用到的亮点
- getopt_long()命令行解析函数的使用
- sched_yield() 主动交出cpu:
 Strategic calls to sched_yield()  can  improve  performance  by  giving other  threads  or processes  a chance to run when (heavily) contended  resources (e.g., mutexes) have been  released  by  the  caller.
- setvbuf() 无缓冲交换pipe数据：
The setvbuf() function may be used on any open stream to change its buffer.  The mode argument must be one of the following three macros:

		_IONBF unbuffered

		_IOLBF line buffered

		_IOFBF fully buffered

> 参考：http://www.cplusplus.com/reference/cstdio/setvbuf/
>
>int setvbuf ( FILE * stream, char * buffer, int mode, size_t size );
Change stream buffering
Specifies a buffer for stream. The function allows to specify the mode and size of the buffer (in bytes).
>
>If buffer is a null pointer, the function automatically allocates a buffer (using size as a hint on the size to use). Otherwise, the array pointed by buffer may be used as a buffer of size bytes.
>
>This function should be called once the stream has been associated with an open file, but before any input or output operation is performed with it.
>
>A stream buffer is a block of data that acts as intermediary between the i/o operations and the physical file associated to the stream: For output buffers, data is output to the buffer until its maximum capacity is reached, then it is flushed (i.e.: all data is sent to the physical file at once and the buffer cleared). Likewise, input buffers are filled from the physical file, from which data is sent to the operations until exhausted, at which point new data is acquired from the file to fill the buffer again.
>
>Stream buffers can be explicitly flushed by calling fflush. They are also automatically flushed by fclose and freopen, or when the program terminates normally.
>
>All files are opened with a default allocated buffer (fully buffered) if they are known to not refer to an interactive device. This function can be used to either redefine the buffer size or mode, to define a user-allocated buffer or to disable buffering for the stream.
>
>The default streams stdin and stdout are fully buffered by default if they are known to not refer to an interactive device. Otherwise, they may either be line buffered or unbuffered by default, depending on the system and library implementation. The same is true for stderr, which is always either line buffered or unbuffered by default.
>


---

# WebBench

Webbench是一个在linux下使用的非常简单的网站压测工具。它使用fork()模拟多个客户端同时访问我们设定的URL，测试网站在压力下工作的性能，最多可以模拟3万个并发连接去测试网站的负载能力。

## 依赖
ctags

## 使用：

	sudo make && sudo make install PREFIX=your_path_to_webbench
  
## 命令行选项：




| 短参        | 长参数           | 作用   |
| ------------- |:-------------:| -----:|
|-f     |--force                |不需要等待服务器响应               | 
|-r     |--reload               |发送重新加载请求                   |
|-t     |--time <sec>           |运行多长时间，单位：秒"            |
|-p     |--proxy <server:port>  |使用代理服务器来发送请求	    |
|-c     |--clients <n>          |创建多少个客户端，默认1个"         |
|-9     |--http09               |使用 HTTP/0.9                      |
|-1     |--http10               |使用 HTTP/1.0 协议                 |
|-2     |--http11               |使用 HTTP/1.1 协议                 |
|       |--get                  |使用 GET请求方法                   |
|       |--head                 |使用 HEAD请求方法                    |
|       |--options              |使用 OPTIONS请求方法               |
|       |--trace                |使用 TRACE请求方法                 |
|-?/-h  |--help                 |打印帮助信息                       |
|-V     |--version              |显示版本号                         |
