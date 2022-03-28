# Chapter1: Get Started

## 单词解释

- stream：流，表示IO设备上输入/输出的一连串的字符；

- built-in type：内置类型（如int，str等）；
- system prompt：系统提示符，例如`$ g++ -o prog1 prog1.cc` 中的`$`；
- aka：Also known as（即是）；
- argument：参数；
- expression：理解为表达式；
- operator：操作符
- Syntax errors：语法错误；
- Type errors：类型错误；
- Declaration errors：声明错误(可能原因：1.未声明namespace；2.标识符拼写错误)；

## Running the Complier from Command Line

- `$ g++ -o prog1 prog1.cc`：
  - `-o prog1`：-o为参数，后面prog1表示输出文件名称(UNIX下没有后缀，Windows下后缀为`.exe`)
  - 如果不指定输出文件名，默认生成`a.out`(UNIX)或`a.exe`(Windows)
- `return 0` & `return -1`

## Input/Output

- 使用的Library：`iostream`

  - `istream`：输入流，代表：`cin`；

  - `ostream`：输出流，代表：`cout`, `cerr`(see-erro), `clog`(see-log)；

    > `cerr`：查看程序运行的erro和warning；
    >
    > `clog`：查看程序运行的输出信息；

- 输入输出程序的执行流程：

  - 代码：`std::cout << "Enter two numbers:" << std::endl;`
  - `<<` 是一个操作符，如第一个`<<`，该操作符分别由左操作数(`std::cout`)和右操作数(`"Enter two numbers:"`)。左操作数`cout`是ostream类型，操作符`<<`先将右操作数的值`"Enter two numbers:"`写给左操作数，最后**输出左操作数(`cout`)到屏幕上**；

  > `endl`：作用是结束当前行(换行作用)，并刷新缓存器(buffer)，确保当前的stream成功输出，避免内存占用。

> 注意：在debug程序时，习惯通过cout输出查看某处程序的变量值。但是若程序崩溃，输出可能滞留在缓存器内，从而导致程序错误推断报错的位置。

- **namespace**：避免标识符名称重复导致的冲突(后面3.1章节会详细展开介绍)
  - `std::` ：是一个前缀，用来表示之后的标识符是定义在`std`这个`namespace`中的。

## 当用`istream/ostream`作为condition时

- 在循环中我们可以用`istream/ostream`类型的变量作为condition，当该类型的变量为**valid**时循环继续，**invalid**时循环退出。

  - 示例代码：

    ```c++
     while (std::cin >> value)
     	sum += value;
    ```

  - **valid**：当我们持续输入整数时，循环会持续下去

  - **invalid**：有两种，一种是收到`End-of-file`的指令，另一种是收到非整型的输入(如str)

  > `End-of-file`：在Windows中是Ctrl+z组合键(输入到命令行上显示为`^Z`)；UNIX中是Ctrl+d组合键

