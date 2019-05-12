* int fflush(FILE *stream)
  - 对输出流来说, fflush 函数将已写入缓冲区但尚未写入文件的所有数据写到文件中.
    对输乎流来说, 其结果是未定义的. 如果在写的过程中发生错误, 则返回 EOF, 否则
    返回0.
  - fflush(NULL) 将清洗所有的输出流.
  - 在读和写的交叉过程中, 必须调用 fflush 函数或文件定位函数.

* getopt()

  #+begin_src c
    int getopt(int argc, char * const argv[], const char *optstring);

    extern char *optarg;
  #+end_src

* strlen() 和 sizeof()

  1. strlen()的一种实现就是遍历字符串，遇到'\0'就终止，因而返回的结果是第一个'\0'前
     字符元素的个数

  2. sizeof 常用来求变量占用内存空间的大小，因而它返回的是存储字符串的变量所占用
     的内存空间大小，用来求字符串的长度，只在特定情况下可行，即字符数组刚好被一
     个字符串占满。


