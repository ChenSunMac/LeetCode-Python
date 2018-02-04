# FILE Operation & Tree

## What is FILE?

- 从用户的角度看，文件可分为普通文件和设备文件两种
    + 普通文件：在磁盘或其它外部介质上的一个有序数据集
    + 设备文件：显示器（stdout），键盘（stdin），打印机，摇杆
- 从文件编码的方式来看： 
    + ASCII码文件 (.txt)
    + 二进制码文件（.bin）
数5678的二进制存储形式为：
    00010110  00101110 两个字节

C系统在处理这些文件时，并不区分类型，都看成是字符流，按字节进行处理，所以叫做stream..

## 文件指针是啥。。
C语言中用一个指针变量指向一个文件，这个指针称为文件指针。
通过文件指针就可对它所指的文件进行各种操作（以后还会提到file descriptor）

其中FILE应为大写，它实际上是由系统定义的一个结构，该结构中含有文件名、文件状态和文件当前位置等信息。在编写源程序时不必关心FILE结构的细节。

## 文件操作函数

- 打开文件
- 关闭文件
- 单个字符输入输出
- 字符串输入输出
    + fprintf(fp,”%d”,i)； 表示将整数变量i的值按%d的格式输出到fp指定的文件上
    + fscanf(fp,”%d”,i)；  表示将fp指定的值按%d的格式读入到整数变量i上
- 整块读写
    + fread函数是从fp所指向的文件中读入count次，每次读size字节，读入的信息存在buffer里
    + fwrite函数将buffer地址开始的信息输出count次，每次写size字节到fp文件中。
- fseek 移动文件指针到特定的地方

## 每行读写
```c
#include <stdio.h>
#include <stdlib.h>
int main(int argc, char *argv[])
 {
   int i,flag=1;
   char str[80],filename[50];
   FILE *fp;
   printf ("please input filename:\n");
   scanf("%s",filename);
   if ((fp=fopen(filename,"w"))==NULL)
     {
       printf ("cannot open!\n");
       exit(0);
     }
   while(flag==1)
     {
       printf ("\ninput string:\n");
       scanf("%s",str);
       fprintf(fp,"%s",str);  //将str字符串内容以%s形式写到fp所指文件上
       printf ("continue:?\n");
       if((getchar()=='N')||(getchar()=='n'))
      flag=0;
     }
   fclose(fp);
   fp=fopen(filename,"r");
   while(fscanf(fp,"%s",str)!=EOF)
     {
       for(i=0;str[i]!='\0';i++)
     if((str[i]>='a')&&(str[i]<='z'))
       str[i]-=32;
       //将小写字母转换为大写字母
       printf ("%s\n",str);
     }
   fclose(fp);
   return 0;
 }
```
