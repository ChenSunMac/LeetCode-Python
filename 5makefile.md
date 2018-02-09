# MAKE FILE 
一般来说，无论是C、C++、还是pas，首先要把源文件编译成中间代码文件，在Windows下也就是 .obj 文件，UNIX下是 .o 文件，即 Object File，这个动作叫做编译（compile）。然后再把大量的 Object File合成执行文件，这个动作叫作链接（link）。

编译时，编译器需要的是语法的正确，函数与变量的声明的正确。对于后者，通常是你需要告诉编译器头文件的所在位置（头文件中应该只是声明，而定义应该放在C/C++文件中），只要所有的语法正确，编译器就可以编译出中间目标文件。一般来说，每个源文件都应该对应于一个中间目标文件（O文件或是 OBJ文件）

# MAKE FILE EXAMPLE

make 是如何工作的呢？ 
默认情况下，我们只输入make 命令，
1. make 会在当前目录下找名字叫 ”makefile“ 或者 "Makefile" 的文件
2. 如果找到，他会找文件中的第一个目标文件，e.g. target，那么在这个例子里就应该是all 所以第一题的答案就是 all 作为最终的目标文件
3. 如果all这个文件不存在，或者all所依赖的后面的dependencies 有修改/不存在，那么就会执行后面的定义去生成最终目标文件
4. 也就是会递归式的生产后面的.o 文件

补充： 从make的第二步发现，最终目标只能有一个，那如果需要生成两个甚至多个exe的时候该怎么办呢？
就是用这里的all，可以看到all是一个特殊的target，我们叫他：一个没有规则的终极目标， 比如
all:main1 main2
所以最终并不会生成一个叫all的文件，

所以第二题我们的答案是 ： printlog.o, message.o, queue.o, printlog.o 
第三题比较简单，可以是 message.o and printlog 
或者
gcc -Wall -g -c message.c, 
gcc -Wall -g -o printlog printlog.o message.o queue.o

# PHONY
一般在我们想删除掉一些中间过程的时候有用
关键字.PHONY 告诉make该目标是“假的”（磁盘上其实没有clean），这时make为生成这个目标就会将其规则执行一次。.PHONY修饰的目标就是只有规则没有依赖
如果没有phony 修饰的话， 目标clean没有任何依赖，make执行时认为这已经到“根上”了（就是认为磁盘上有clean，就像main2.c），将其忽略。



