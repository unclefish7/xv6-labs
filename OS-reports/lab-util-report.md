# Lab: Xv6 and Unix utilities相关实验报告

## 1. Boot xv6

### 实验目的

在Ubuntu环境下运行xv6。并掌握xv6的基础使用方法

### 实验步骤

1. 在克隆下来的xv6-labs-2021仓库中，执行：

   ```cmd
   $ git checkout util
   ```

   这样就切换到了专门用于该实验的环境。

1. 尝试构建并运行xv6：

   ```cmd
   $ make qemu
   riscv64-unknown-elf-gcc    -c -o kernel/entry.o kernel/entry.S
   ...
   
   xv6 kernel is booting
   
   hart 2 starting
   hart 1 starting
   init: starting sh
   $ 
   ```

1. 尝试使用`ls`命令：

1. 使用Ctrl-a 以退出qemu

### 遇到的问题以及解决方法

- `make qemu`命令必要在`/xv6-labs-2021`这个根目录下运行，否则会报错。

### 总结与体会

该实验主要目的除了熟悉xv6的基本操作以外，也是为了测试xv6环境搭建是否正确。并且这也是第一次在linux环境下进行项目的搭建，linux相关的知识也是学习了不少（比如：linux目录结构，用户创建与切换，使用命令行进行git clone等操作）

## 2. sleep

### 实验目的

在xv6下构建一个sleep程序，使得整个系统能够停止特定的一段时间（tick数由用户指定）。

### 实验步骤

1. 源代码放在`user/sleep.c`下。

1. 编写源代码：

   ```c
   #include "kernel/types.h"
   #include "user/user.h"
   
   int main(int argc, char *argv[]) {
       if (argc != 2) { //传入的参数个数必须是两个
           printf("Usage: sleep <ticks>\n");
           exit(1);
       }
       int ticks = atoi(argv[1]); //把字符串转化为整数
       sleep(ticks);//让系统陷入睡眠
       exit(0);
   }
   
   ```

   > main函数中的argc代表传入参数的个数，*argv[]内部是每个被传入的参数

1. 在`Makefile`文件中添加sleep函数

1. 在xv6环境中运行sleep，查看是否符合预期。

1. 运行测试程序`$ make GRADEFLAGS=sleep grade`，查看运行结果是否正确

### 遇到的问题以及解决方法

- 第一次尝试编写xv6程序，不知道如何接收命令行的参数：知道argc，argv的含义之后就知道怎么编写程序了。

### 总结与体会

该实验有助于我理解xv6环境下程序是如何编写，编译，运行的。同时加深我对C语言一些特性的认知。
